# ALUFullFile

Lab 4 ALU FIles

//2's Compliment

module Twos_Compliment(B, out1);


input [31:0] B;

output [31:0] out1;

reg [31:0] result;

assign out1 = result;


always @(*)

begin

	result = ~B + 1;
  
end

endmodule 


//Adder

module Adder(Data0, Data1, out3);

input [31:0] Data0, Data1;

output [31:0] out3;

reg [31:0] result;

assign out3 = result;

always @(*)

begin

	result = Data0 + Data1;
end

endmodule 

//Mux

module ALU_Mux(Data0, Data1, out2, sel);

input [31:0] Data0, Data1;

input [0:0] sel;

output [31:0] out2;


reg [31:0] result;

assign out2 = result;

always @(*)

begin

		case(sel)
    
		1'b0:
    
			result = Data1;
      
			
		1'b1:
    
			result = Data0;
      
			
		default: result = Data0;
    
		
		endcase
    
	end
  
endmodule

//ALU 

module ALU(A, B, sel, out0);


input [31:0] A,B;

input [2:0] sel;

output [31:0] out0;


reg [31:0] result;

assign out0 = result;

Twos_Compliment dut2(B, outC);

ALU_Mux dut1(outC, B, outB, sel1);

Adder dut0(outB, A, outA);


always@(*)

begin

	case(sel)
  
	3'b000: //add
  
		result = outA;
    
		
	3'b001: //xor
  
		result = A ^ B;
    
		
	3'b010: //and
  
		result = A & B;
    
		
	3'b011: //or
  
		result = A | B;
    
		
	3'b010: //nor
  
		result = ~(A | B);
    
		
	3'b101: //shift left
  
		result = A<<1;
    
		
	3'b110: //shift right
  
		result = A>>1;
    
		
	default: result = A + B;
  
	
	endcase
  
end

endmodule 


//Testbench

`timescale 1ns / 1ps  


module ALU_tb;

//Inputs

 reg[31:0] A,B;
 
 reg[2:0] sel;
 

//Outputs

 wire[31:0] out;
 

 // Verilog code for ALU
 
 integer i;
 
 ALU dut(A, B, sel, out);
 
    initial begin
    
    // hold reset state for 100 ns.
    
      A = 8'h0A;
      
      
      B = 4'h02;
      
      
      sel = 4'h0;
      
      
      for (i=0;i<=6;i=i+1)
      
      begin
      
       sel = sel + 8'h01;
       
       #10;
       
      end;
      
      
      A = 8'hF6;
      
      B = 8'h0A;
      
      
    end
    
endmodule 
