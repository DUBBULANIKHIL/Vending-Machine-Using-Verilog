# Vending-Machine-Using-Verilog
//Design for Vending machine
//c=0  ->Sending cents.
//c=1  ->pressing button.
//s0=idle state
//s1=25 cent.
//s2=50 cent.
//s3=75 cent.
module ven_mach(input c,input clk,input rst,output reg y);
  reg [1:0]ps;
  reg [1:0]ns;
parameter s0=2'b00,
          s1=2'b01,
          s2=2'b10,
          s3=2'b11;
 always @(posedge clk or negedge rst)
 begin
   if(!rst)
    ps<=s0;
   else
    ps<=ns;
 end
  always @(ps or c)
  begin  
   case(ps)
   s0:
     if(c==0)
     begin
     ns=s1;
      y=0;
     end
     else
     begin
     ns=s0;
     y=0;
     end
  s1:
   if(c==0)
     begin
     ns=s2;
      y=0;
     end
     else
     begin
     ns=s1;
     y=0;
     end
   s2:  
   if(c==0)
     begin
     ns=s3;
      y=0;
     end
     else
     begin
     ns=s2;
     y=0;
     end
   s3:
     //In state s3,initially input is 0,it means 100 cents extra cents are returned back and stays in the same state.
     //In state s3,initially input is 1,after input is 0 or directly 1,juice comes out and stays in the same state.
     //In state s3,initially input is 0 after input is 1,it means juice has come out and same cycle should begin again and the next state will be s1 where 25 cents are present.
     if(c==0) 
     begin
     ns=s3;
      y=0;
     end
     else if(c==1)
     begin
     ns=s3;
     y=1;
     end
     else if(c==0)
     begin
     ns=s1;
     y=0;
     end
   endcase
  end
  endmodule
      
      
  
