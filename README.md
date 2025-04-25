# cs3220-lab-3-solved



**<span style='color:red'>TO GET THIS SOLUTION VISIT:</span>** https://www.ankitcodinghub.com/product/cs3220-lab-3-10-pts-solved/

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;128045&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;4&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (4 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS3220 Lab #3 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">
            
<div class="kksr-stars">
    
<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
    
<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>
                

<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (4 votes)    </div>
    </div>
10 pts in total, will be rescaled into 11.25% of your final score of the course.

Part 0: Env Setup: 0 pts

Part 1: Deploy on Pynq-Jupyter: 10 pts

Submission ddl: Oct 9nd

This lab serves as a continuation of Lab #2. The primary aim is to guide you through the process of deploying your RISC-V processor on a Pynq board.

Learning Outcomes:1. Learn to create and use AXI lite protocol to communicate with your RISC-V processor.

2. Get familiar with Vivado and Vitis HLS toolchain.

Part-0: Env Setup (0 pts)

Accessing Pynq Board

We’ve settled remote access to the pynq board. Please follow the instructions outlined in this: document.

Setting up the environment might take some time. Kindly be patient.

Remote Desktop

Updalod &amp; Download Files

You can access the root directory of your remote machine through your browser. Refer to step 4 of the above document, click on the “data root directory” at the bottom of the screen. The remote desktop and pynq board share the same data storage, so it is not needed to transfer data between them.

Part-1: Deployment on Pynq-Jupyter (10pts)

In this part, you will deploy your RISC-V processor on a pynq board. The pynq board provides a field programmable gate array, which allows you to program its hardware. You will be able to communicate with the board through AXI lite protocol with a Jupyter notebook.

Step-1: Vitis for Creating a Communication Adapter

In this step, you will generate a communication adapter using comm.cpp in Vitis HLS. This allows you to communicate with the verilog modules (your RISC-V processor).

The code comm.cpp only defines ports (inputs and output arguments) to verilog modules with memory-mapped connection using AXI lite protocol. So you can consider this vitis code as an communication adapter, and vitis generates most of the necessary logics for us.

Step-2: Vivado for Bitstream Generation

[1] Prepare your codes:

Modify the pipeline.v to have two additional ports and change reset to rest_n, you will interact with it from the CPU side (Jupyter Notebook) through these ports.

Before:

module pipeline ( input wire clk, input wire reset );

After:

“` module pipeline( input clk, input reset_n, output[31:0] out1, output[31:0] out2 );

wire reset = ~reset_n; “`

In pipeline.v, connect out1 for cycle_count:

“` always @ (posedge clk) begin if (reset) begin cycle_count &lt;= 0; end else begin cycle_count &lt;= cycle_count + 1; end end assign out1 = cycle_count; “`

assign out2 = 32’d33; [2] Create a block design

First create a vivado project and a block diagram. Then import the IP repo (the communication adapter) generated in step-1, and add the comm IP to the block diagram.

Please see this link for a step by step demonstration.

[3] Add the RISC-V processor to the block diagram.

[4] Connect pipeline

You will need to connect your RISC-V processor with the communication adapter (in1 in common &lt;-&gt; out1, in2 in common &lt;-&gt;out2) manually.

[5] Add Zynq PS module from IP repo and then use auto-connect features to complete all the connections.

The procedure for adding zynq ps is the same as how you add the comm IP into the block diagram (you do not need to import a repo for zynq ps, Vivado automatically loaded it for you), as demonstrated in the video above. The PS stands for the on-chip processing system (where you run the jupyter notebook), which will communicate with the RISC-V processor through the AXI lite ports.

The autoconnect button shows up at the top of the block diagram. Click “Run Connection Automation” and then select all modules, then click OK.

If clock or reset signal connections are missing, you can connect them manually. The final output should be as follows:

[6] Create HDL wrapper

Go to â€œSourcesâ€ panel and right click on your block design name, click on â€œCreate HDL wrapperâ€. Click on â€œLet Vivado manage wrapper and auto-updateâ€ option and click on â€œOKâ€.

Make the design_wrapper as a top module by right click it in the source code and choose “Set as Top”.

[7] Synthesize/implementation/generate bitstreams

Go to the “Flow Navigator” panel and click “Generate Bitstream” (it will ask to synthesize etc., click yes). The bitstreams is used to tell the FPGA how to program its hardware.

The bistream generation takes around 10 mins, in the bottom of the screen, if you select “Design Runs”, you can see the progress. [9] Export the bitstream

Click on File -&gt; Export -&gt; Export bitstream.

[10] Prepare the files

Copy the following files: + [proj_name].runs/impl_1/design_1_wrapper.bit or where you expored the bitstream in step [9]. + [proj_name].runs/impl_1/design_1_wrapper.tcl + [proj_name].gen/sources_1/bd/design_1/design_1.hwh.

Make sure you rename all the files to have the same name (e.g. riscv.bit, riscv.tcl, riscv.hwh)

Step-3: Deploy on the Pynq Board

[11] Upload the files

Place all the generated files in the above step and the riscv_test.ipynb file in a same folder.

[12] Running on the Pynq Board

Open the riscv_test.ipynb file on the requested Jupyter notebook and run the code, the 0x20 address corresonds to out1 and 0x30 address corresponds to out2, out1 value will keep changing since it’s a cycle count and out2 value will be the constant you put in the beginning of step 2. include the screenshot of ipynb on your report

Submission Guideline

What to submit

A zip file containing your .bit, .tcl, .hwh files; A screenshot of the jupyter notebook, showing the expected value in step [12].

Grading policy

If the bitstream you submit can be successfully deployed on the pynq board and the screenshot in step [12] is correct, you will receive full credit.
