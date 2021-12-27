// COMP3361
import java.lang.Math.*;

public class DFT {

   public static void main(String[] args) {
      int[] x1 = {-1, -1, -1, 0, 0, 0}; // Test cases
      int[] y1 = {0, 0, -1, -1, -1, 0};
      
      
      ComplexNumber[] result = DFTSolver.solve(x1); // Constructs an array of complex numbers complex numbers and passes the test case through the static method
      
      for(int i = 0; i < result.length; i++){ // This part of the main method takes each index of the complex number array an prints an appropriate answer according to which pieces of the complex number remain
         System.out.print("x[" +i+ "] = ");
         if(result[i].real == 0 &&result[i].img == 0 ){
         System.out.println(0);
         System.out.println();
        }else{
        if(result[i].real != 0){
            System.out.print(result[i].real);
        }
        if(result[i].real != 0 &&result[i].img != 0 ){
         System.out.print(" + ");
        }
        if(result[i].img != 0){
         System.out.print("i" + result[i].img);
        }
        System.out.println(" / " + result.length);
        System.out.println();
      }
      }
      
      ComplexNumber[] result1 = DFTSolver.solve(y1); // Second test case
      
      for(int i = 0; i < result.length; i++){
         System.out.print("y[" +i+ "] = ");
         if(result1[i].real == 0 &&result1[i].img == 0 ){
         System.out.println(0);
         System.out.println();
        }else{
        if(result[i].real != 0){
            System.out.print(result1[i].real);
        }
        if(result1[i].real != 0 &&result1[i].img != 0 ){
         System.out.print(" + ");
        }
        if(result1[i].img != 0){
         System.out.print("i" + result1[i].img);
        }
        System.out.println(" / " + result1.length);
        System.out.println();
      }
      }
      
      
      
   }
   
   public static class DFTSolver{ 
      
      
      public static ComplexNumber[] solve(int[] input) { // Takes in an array of -1/0/1
      
         double sum = 0;
         ComplexNumber cnSums = new ComplexNumber(0, 0);// acts as the sum of all complex numbers in a single loop
         ComplexNumber[] result = new ComplexNumber[input.length];
         
         for(int i = 0; i < input.length; i++){ // Parses through each x[k] value
            for(int j = 0; j < input.length; j++) {  // parses through each index of x[n]
               if (2*Math.PI*i*j/input.length == 0){ // if the e exponent is equal to zero, add the x[n] value to the sum
                  sum += input[j];
                  
               } 
               if(2*Math.PI*i*j/input.length != 0 && input[j] != 0) { // If not, instantiates a complex number object and sums it with the running complex number
                  ComplexNumber r = new ComplexNumber(input[j] * Math.cos(-2*Math.PI*i*j/input.length), input[j] * Math.sin( -2*Math.PI*i*j/input.length));
                  cnSums = ComplexNumber.sum(cnSums, r);
               }
           }
           result[i] = cnSums; // sets array index of x[n] equal to the complex number sum
           cnSums = new ComplexNumber(0, 0); // resets the sum count
           result[i].realSum(sum);// sums the real number value of the complex number with the -1/1s gathered from 0 exponent e values
            if(-0.01 < result[i].real  && result[i].real < 0.01){// removes microscopic values (real or imaginary) from the complex number
            result[i].setReal(0);
            }
            if(-0.01 < result[i].img  && result[i].img < 0.01){
               result[i].setImg(0);
            }
           sum = 0;
           System.out.println();
         }
         return result; // returns the complex number array
      }
   }
   
   public static class ComplexNumber{
   //for real and imaginary parts of complex numbers
   double real, img;
	
   //constructor to initialize the complex number
   ComplexNumber(double r, double i){
	this.real = r;
	this.img = i;
   }
	
   public static ComplexNumber sum(ComplexNumber c1, ComplexNumber c2)
   {
	//creating a temporary complex number to hold the sum of two numbers
        double sumr = c1.real + c2.real;
        double sumi = c1.img + c2.img;
        
        ComplexNumber sum = new ComplexNumber(sumr, sumi);
        
        //returning the output complex number
        return sum;
    }
    
    public void realSum(double in){ // sums the real number value of the complex number with the -1/1s gathered from 0 exponent e values
      real += in;
    }
    
    public void setReal(double realIn){ // Setter
      real = realIn;
    }
    
    public void setImg(double imgIn){ // Setter
      img = imgIn;
    }
    
}



}
