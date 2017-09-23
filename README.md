# AFD
package afd;

/*
Yanelli Decire López Estradda   150822
E(r)= 1(00*)*

Para facilitar el proceso de programación utilicé la matrz de adyacencia para
ver a donde me mandaba cada método si se ingresaba 1 o 0 y poder observar 
en donde habia aceptaciones
*/

public class AFD {
    
    int cont;
    char []car;
    boolean aceptado;

    public static void main(String[] args) {
        
        AFD aut = new AFD();
        String cadena ="10";//aqui declaro una cadena cualquiera para ver si funciona mi códigoo
        aut.car= cadena.toCharArray();
        aut.inicio();
        if(aut.aceptado){
            System.out.println("Cadena Aceptado");
        }
        else {
            System.out.println("Cadena No aceptado");
        }
    }
    
    public void inicio(){
        cont=0;
        aceptado=false;
        q0();
    }
    
    public void q0(){
        System.out.println("q0");
        if(cont<car.length){
            if(car[cont] =='0'){
                cont++;
                qerror();//Segun el lenguaje el primer caracter debe ser 1 por lo que al ingresar un cero de tiene ue ir a error
            }
            else if(car[cont]=='1'){
                cont++;
                aceptado=true;//Como la concatenacion es asterisco puede o no pueden ir los 0's por lo que si se ingresa minimo un 1 el estado debe cambiar a aceptado
                q1();//se manda a q1 pafra ver si tiene mas elementos
            }
        }
    }
    
    public void q1(){
        System.out.println("q1");
        if(cont<car.length){
            if(car[cont] =='1'){
                cont++;
                qerror();//Debido a que en el lenguaje despues del 1 van puros 0's si se ingresa otro 1 debe ser error
            }
            else if(car[cont]== '0' || car[cont]== ('0' + ' ') ){
                cont++;
                q2();//0 es un caracter en la cadena por lo que se manda a otro estado para seguir validando 
            }
        }
    }
    
    public void q2(){
        System.out.println("q2");
        if(cont<car.length){
            if(car[cont] =='0'){
                cont++;
                q2();//Ya que este 0 es asterisco puede ser ingresado varias veces y or eso se manda nuevamente a q2
                aceptado=true;//el estado es aceptado ya que pueden ir n ceros 
            }
            else if(car[cont]=='1'){
                cont++;
                qerror();//Debido a que en el lenguaje despues del 1 van puros 0's si se ingresa otro 1 debe ser error
            }
        }
    }
    
    public void qerror(){
        System.out.println(" error ");
        aceptado=false;
    }
    
}
