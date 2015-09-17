# Torteria-equipo-Cafe


//EQUIPO CAFE

#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<locale.h>
#define s scanf
#define p printf

struct menu{
int cantidad,costo,cantidadt;	
};

main()
{
	setlocale(LC_ALL,"esm");
	char sel, cin[100];
	int suma=0,sum_his=0,i,aux,num_ticket=0,sumat=0;
	FILE *arch,*archuno,*archdos,*archtres;
    
    archtres=fopen("factura.txt","w");
    fclose(archtres);
    
    
	system ("color f0");
	struct menu c[4];
	
	for(i=0;i<4;i++) //Declaración de cantidades del menu
	    {
		c[i].cantidad=0;
		c[i].cantidadt=0;
	    }
  do
    {                 
     p("\n Total es de: %d\n\n", suma);
             //Esta parte del codigo se hace para la seleccion
        do
          { 
            arch=fopen("datos.txt","r");	//apertura de archivos
	        if (arch==NULL)                 
	    		 p("ERROR");
		    else
				{
		        while(feof(arch)==NULL)       //Verificar hasta que termine el archivo
		             {
		             fgets(cin,3,arch);  //hace grupos de dos caracteres
		                aux=atoi(cin); //transformación de char a int
						if(aux==40)
						   c[0].costo=aux;
						if(aux==15)
						   c[1].costo=aux;
						if(aux==55)
						   c[2].costo=aux;
						if(aux==10)
						   c[3].costo=aux;
						p("%s",cin);		   
		             }
		          fclose(arch);
	              }
   
		  p(" \n\nSeleccione que desea en su orden: " );   //Desicion de selección
          fflush(stdin);  
          sel=getchar();
          system("CLS");
          } while(sel!='a'&& sel!='A' && sel!='b'&& sel!='B'&& sel!='c'&& sel!='C'&& sel!='d'&& sel!='D'&& sel!='e'&& sel!='E');                //la seleccion tiene que estar entre 0 y 7 
        
        if(sel=='e' || sel=='E') 
		  {   
		   num_ticket++;
		   archuno=fopen("ticket.txt","w"); 
		   fprintf(archuno,"\n\n\n Ticket   %d",num_ticket);
		   fprintf(archuno,"\n\n Tu pedido fue el siguiente:\n");      //Contador del pedido en cuanto al menu
       	   fprintf(archuno,  "-------------------------\n"   );       
           fprintf(archuno," %d Cubana   \n", c[0].cantidad);
           fprintf(archuno," %d Jamon    \n", c[1].cantidad); 
           fprintf(archuno," %d Especial \n", c[2].cantidad); 
		   fprintf(archuno," %d Refresco \n", c[3].cantidad);                   
           fprintf(archuno,"\n El monto a pagar es de: %d\n\n", suma);
           fclose(archuno);
           
           archtres=fopen("factura.txt","r+"); 
           fseek(archtres,0,SEEK_END);
		   fprintf(archtres,"\n\n\n Ticket   %d",num_ticket);
		   fprintf(archtres,"\n\n Tu pedido fue el siguiente:\n");      //Contador del pedido en cuanto al menu
       	   fprintf(archtres,  "-------------------------\n"   );       
           fprintf(archtres," %d Cubana   \n", c[0].cantidad);
           fprintf(archtres," %d Jamon    \n", c[1].cantidad); 
           fprintf(archtres," %d Especial \n", c[2].cantidad); 
		   fprintf(archtres," %d Refresco \n", c[3].cantidad);                   
           fprintf(archtres,"\n El monto es: %d\n\n", suma);
           fclose(archtres);
           p("\n\n\t\tEn breve obtendra su ticket\n"
			 "\n\n\t\tFUE UN PLACER ATENDERLE\n");
		   p(" \n\nPresione ENTER para obtener la cuenta y despues presione R para regresar o Q para terminar el dia " );   //Desicion de selección
              fflush(stdin);  
              sel=getchar();
			
			if(sel=='r' || sel=='R') 
			  {
			   system("CLS");
			   
			   	for(i=0;i<4;i++) //Declaración de cantidades del menu
	               c[i].cantidad=0;
	               suma=0;
	             p("\n Total es de: %d\n\n", suma);  
			     do
                    { 
                	arch=fopen("datos.txt","r");	//apertura de archivos
	                if (arch==NULL)                 
	    		       p("ERROR");
			        else
				       { 
		                while(feof(arch)==NULL)       //Verificar hasta que termine el archivo
		                     {
		                      fgets(cin,3,arch);  //hace grupos de dos caracteres
		                        aux=atoi(cin); //transformación de char a int
								if(aux==40)
								   c[0].costo=aux;
								if(aux==15)
								   c[1].costo=aux;
								if(aux==55)
								   c[2].costo=aux;
								if(aux==10)
								   c[3].costo=aux;
						       p("%s",cin);		   
		                     }
		                fclose(arch);
	                   }
          p(" \n\nSeleccione que desea en su orden: " );   //Desicion de selección
          fflush(stdin);  
          sel=getchar();
          system("CLS");
          } while(sel!='a'&& sel!='A' && sel!='b'&& sel!='B'&& sel!='c'&& sel!='C'&& sel!='d'&& sel!='D'&& sel!='e'&& sel!='E');                //la seleccion tiene que estar entre 0 y 7 
        }
}

	    
	    if(sel=='q'||sel=='Q')
		    { 
			archdos=fopen("ventasdia.txt","w"); 
			fprintf(archdos,"\n\n\n ventas totales   %d",num_ticket);
       		fprintf(archdos,  "\n-------------------------\n"   );       
        	fprintf(archdos," %d Cubana   \n", c[0].cantidadt);
        	fprintf(archdos," %d Jamon    \n", c[1].cantidadt); 
        	fprintf(archdos," %d Especial \n", c[2].cantidadt); 
			fprintf(archdos," %d Refresco \n", c[3].cantidadt); 
			fprintf(archdos,"\n La ventas del dia son de: %d\n\n", sumat);
	        fclose(archdos);
	        break;
			}
            
            
    switch(sel) //Sel sirve de bandera para tomar desiciones
	      {
		   case 'a': case'A':    
			suma+=c[0].costo;
			sumat+=c[0].costo;
			c[0].cantidad++;
			c[0].cantidadt++;				
	        break;
	        
	        case 'b': case'B':
			suma+=c[1].costo;
			sumat+=c[1].costo;
			c[1].cantidad++;
			c[1].cantidadt++;
    		break;
    		
    		case 'c': case'C':
			suma+=c[2].costo;
			sumat+=c[2].costo;
			 c[2].cantidad++;
			 c[2].cantidadt++;
			break;
			
			case 'd': case'D':
			suma+=c[3].costo;
			sumat+=c[3].costo;
			 c[3].cantidad++;
			 c[3].cantidadt++;
	        break;
	        default:
			break;
	       }
	}while(sel);
	
}
