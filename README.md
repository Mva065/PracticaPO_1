# PracticaPO_1

package Exercici1;
import Keyboard.*;
public class Exercici1 {
	
	public static void main(String [] args){
	
		System.out.println("Indica les dimensions del taulell. Entra un numero de files");
		int i = Keyboard.readInt();
		System.out.println("Entra un numero de columnes");
		int j = Keyboard.readInt();
		int v = 0;
		while (i > 10 || j > 10){
			System.out.println("Entra una dimensió de taulell vàlida");
			i = Keyboard.readInt();
			j = Keyboard.readInt();
		}		
		char [][] taulell = new char [i][j];
		creaTaulell(i, j, taulell);
		System.out.println("Especifica un número màxim de tirades: ");
		int ti = Keyboard.readInt();
		int h = 1;
		int l = 0;
		while (ti <= 0){
			System.out.println("Ha de ser major de 0");
			ti = Keyboard.readInt();
		} while (h <= ti){
		tirades(i, j, taulell, ti, v);
		if (totesParades(taulell, i, j)){
			System.out.println("Felicitats, Has completat el joc.");
		} else {
			System.out.println();
		} h++;
		}
		if (h >= ti){
			System.out.println("Mala sort. Ja no tens més tirades. El joc ha acabat");
			while (l < ti){
				enap(i, j, taulell, ti, v, l);
				l++;
			}	
		}

	} public static void creaTaulell(int i, int j, char [][] taulell) {
		
		int t = 0;
		int ali = 0;
		int alj = 0;
		char ences = '■';
		char apagat = '□';
		int numB;
		
		for (int x=0; x < i; x++) {
		for (int y=0; y < j; y++) {					//Crea el taulell amb totes les bombetes apagades
			    taulell[x][y] = apagat;
	}
	}
		while (t <= 10){
			ali = (int) (Math.random() * i);		//Encen 10 Bombetes
			alj = (int) (Math.random() * j);
			taulell[ali][alj] = ences;
			t++;
	}
		System.out.println("Indica quantes bombetes vols encendre. Indica un numero entre 0 i 10. Com més n'encenguis més dificultat.");
		numB = Keyboard.readInt();
		while(numB < 0 || numB > 10){
			System.out.println("Indica un numero entre 0 i 10");
			numB = Keyboard.readInt();
		} t = 0;
		while (t < numB){
			ali = (int) (Math.random() * i);
			alj = (int) (Math.random() * j);
			System.out.println("Encenem la posició: " + ali + "," + alj);
			if (taulell[ali][alj] == ences){
				taulell[ali][alj] = apagat;
			} else if (taulell[ali][alj] == apagat){
				taulell[ali][alj] = ences;
			}
			t++;
	}
		impresioT(taulell);

	} public static void tirades (int i, int j, char [][] taulell, int ti, int v){
		
		char ences = '■';
		char apagat = '□';
		
			System.out.println("Indica les coordenades del botó a premer");
			System.out.println("Indica la fila. Especifica un valor en l'interval [0,"+ (i - 1) +"]");
			int k = Keyboard.readInt();
			while (k < 0 || k > i){
				System.out.println("Indica un número dins l'interval.");
				k = Keyboard.readInt();
			}
			System.out.println("Indica la columna. Especifica un valor en l'interval [0,"+ (i - 1) +"]");	
			int l = Keyboard.readInt();
			while (l < 0 || l > j){
				System.out.println("Indica un número dins l'interval.");
				l = Keyboard.readInt();	
			} 
			
			impresioT(taulell);	
			
			/*
			 * 	k+1 = sota
			 * 	k-1 = amunt
			 * 	l-1 = dreta
			 * 	l+1 = esqueraa
			 */
			
			
			if (k == 0 || l == 0){

				if(k == 0 && l == 0){	//punta de dalt-esquerra

				if(taulell[k][l] == ences){
				taulell[k][l] = apagat;
				} else {
				taulell[k][l] = ences;}
				
				if(taulell[k+1][l] == ences){
				taulell[k+1][l] = apagat;
				} else {
				taulell[k+1][l] = ences;}
				
				if(taulell[k][l+1] == ences){
				taulell[k][l+1] = apagat;
				} else {
				taulell[k][l+1] = ences;}
				}} else {
				
			if(taulell[k][l] == ences){
				taulell[k][l] = apagat;				
			} else {
				taulell[k][l] = ences;}
			
			if(taulell[k+1][l] == ences){
				taulell[k+1][l] = apagat;			
			} else {
				taulell[k+1][l] = ences;}
			
			if(taulell[k-1][l] == ences){			
				taulell[k-1][l] = apagat;
			} else {
				taulell[k-1][l] = ences;}
			
			if(taulell[k][l-1] == ences){
				taulell[k][l-1] = apagat;			
			} else {
				taulell[k][l-1] = ences;}				
			
			if(taulell[k][l+1] == ences){			//la de la dreta
				taulell[k][l+1] = apagat;
			} else {
				taulell[k][l+1] = ences;}
				}
					
	} public static void impresioT(char [][] taulell){
		
		for (int x=0; x < taulell.length; x++) {
			for (int y=0; y < taulell[x].length; y++) {
				System.out.print (taulell[x][y] + " ");
				}
				System.out.println();
				}
		
	} public static boolean totesParades(char [][] taulell, int i, int j){
		
		int cont = 0;
		char apagat = '□';
		for (int x=0; x < taulell.length; x++) {
			for (int y=0; y < taulell[x].length; y++) {
				if (taulell[x][y] == apagat){
					cont++;
				}
				}}
		if (cont == (i * j)){
			return true;
		} else { 
			return false;
		}
		
	} public static void enap (int i, int j, char [][] taulell, int ti, int v, int l){
		
		char ences = '■';
		char apagat = '□';
		int [] apagades = new int [ti];
		int [] enceses = new int [ti];
		int contenceses = 0, contapagades = 0;
		
		for (int x=0; x < i; x++) {
			for (int y=0; y < j; y++) {
				    if(taulell[x][y] == apagat){
				    	contapagades++;
				    } else if (taulell[x][y] == ences){			//Contador enceses / apagades
				    	contenceses++;
				    }
	}}
		apagades[v] = contapagades;
		enceses[v] = contenceses;
		v++;
		System.out.println("Tirada " + (l+1) + ": --> Tens " + enceses[l] + " enceses i " + apagades[l] + " apagades");
		
		
	} 
	
	
	
	
	
	
	
	
	
	
}

