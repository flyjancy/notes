# Verilog on MacOS

## 准备

为了在macOS上完成简单的Verilog仿真及综合，首先需要安装以下内容:
- iverilog
- Scansion
- yosys
- graphviz

其中iverilog，yosys和graphviz可以通过Homebrew安装，Scansion可以在[其官网](http://www.logicpoet.com/scansion/)下载并安装。

## 仿真流程

iverilog和Scansion安装完成之后，通过Makefile脚本化仿真流程。
Makefile示例脚本如下:

```
RC="Adder32_1"
TB ="Adder32_1_tb"
all:
	iverilog -o wave $(SRC).v $(TB).v
	vvp -n wave
	open -a Scansion wave.vcd
```

为了生成波形，需要在testbench中添加以下代码:

```
/*iverilog */
initial
begin            
    $dumpfile("wave.vcd");        //生成的vcd文件名称
    $dumpvars(0, led_demo_tb);    //tb模块名称
end
/*iverilog */
```

如果不加这几行iverilog编译器专用的语句，将无法生成wave.vcd波形。

完成后，在工程目录下输入`make`即可打开Scansion界面，之后便可以添加信号查看波形了。

注：在终端输入`iverilog`回车，可以看到常用参数使用方法的简单介绍。另外，iverilog还可以把用Verilog HDL编写的.v文件转换成VHDL语言编写的.vhd文件，使用命令`iverilog -tvhdl -o test.vhd test.v`

## 综合

首先编写以下综合命令:

```
# read design
read_verilog counter.v
hierarchy -top counter
# high-level synthesis
proc; opt; fsm; opt; memory; opt; #techmap; opt;
write_verilog synth.v
```

将上述命令保存为show_rtl.ys文件，在终端下执行命令完成综合。

```
yosys show_rtl.ys
```

综合完成后会生成synth.v文件，这是综合后的网表。

生成dot文件:

```
yosys -p "prep; show -stretch -prefix counter -format dot" counter.v
```

生成png图片:

```
dot counter.dot -T png -o counter.png
```

## 总结

基于以上相关工具，便可以在macOS上写一点简单的verilog，用于验证一些小的idea还是非常方便的。