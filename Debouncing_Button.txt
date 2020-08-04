module debounce(input pb_1,clk,output pb_out);
wire Q1,Q2,Q2_bar;
my_dff d1(clk, pb_1,Q1 );
my_dff d2(clk, Q1,Q2 );
assign Q2_bar = ~Q2;
assign pb_out = Q1 & Q2_bar;
endmodule
module my_dff(input DFF_CLOCK, D, output reg Q);
always @ (posedge DFF_CLOCK) 
begin
Q <= D;
end
endmodule





module tb_button;
reg pb_1;
reg clk;
wire pb_out;
debounce uut(.pb_1(pb_1),.clk(clk),.pb_out(pb_out));
initial begin
clk = 0;
forever #10 clk = ~clk;
end
initial 
begin
pb_1 = 0;
#52;
pb_1=1;
#1;
pb_1 = 0;
#1;
pb_1=1;
#1; 
pb_1 = 0;
#1;
pb_1=1;
#2;
pb_1 = 0;
#1;
pb_1=1;
#50; 
pb_1 = 0;
end      
endmodule