module Controlador_7_Seg
(
input wire [5:0] dato_Temp,
input wire [1:0] Est_actual,
input wire Clock,
output reg [6:0] seg_7_catodos,
output reg [3:0] an
 );

localparam [1:0]   zero = 2'b00,
                   Estado_Actual = 2'b01,
                   Decenas = 2'b10,
						 unidades = 2'b11; 

reg [1:0] contador;
wire [6:0] dec , unid, estado;

Deco_de_temp_decenas decenas(dato_Temp,dec); // tercer display
Deco_de_temp_unid Unidades (dato_Temp,unid); // cuarto display 
deco_de_est_maq decomaquina(Est_actual,estado);

always@(posedge Clock)
begin 
   an <= 4'b0000;
   seg_7_catodos <=7'b0000000;
	
	case (contador)
	Estado_Actual:
				   begin
					 // segundo display
					seg_7_catodos <= estado;
					an  <= 4'b1101;
					contador <= 2'b10;
					end 
	 Decenas:
		         begin 
					seg_7_catodos <= dec;
               an <= 4'b1011;
		         contador <= 2'b11;
		         end 
	unidades:
		         begin 
					seg_7_catodos <= unid;
					an <= 4'b0111;
		         contador <= 2'b00;
					end
	zero :   
	            begin  // primer display 
					seg_7_catodos <= 7'b0110000;
					an <= 4'b1110;
		         contador <= 2'b01;
					end
   endcase
	end
endmodule
