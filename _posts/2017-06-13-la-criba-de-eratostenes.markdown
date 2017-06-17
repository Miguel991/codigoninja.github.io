---
title: "Codeando números primos"
layout: post
date: 2017-06-13 19:50:04 -0300

---

### La criba de Eratóstenes

Supongamos que queremos realizar una lista de todos los números primos(hasta ahora imposible) o por lo menos algunos de ellos, por ejemplo los números primos entre 2 y 100 mil. Para esto vamos a seguir un algoritmo hecho tres siglos antes de Cristo en Alejandría por el griego Eratóstenes, el cual funciona de la siguiente manera. Colocamos los números del 2 al 120 en una lista, se toma el primer elemento de la lista en este caso el 2 y se elimina de la lista todos sus múltiplos, luego tomamos el siguiente de la lista y volvemos a eliminar todos sus múltiplos y así sucesivamente hasta recorrer toda la lista, los elementos que queden finalmente en la lista serán nuestros numero primos.

Números Primos: los números primos son aquellos números naturales que no tienen divisores, mas allá de si mismo y de 1.

Veamos la siguiente imagen para entender mejor como funciona el algoritmo de Eratóstenes.

![Criba Eratóstenes](https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif)


El siguiente código java es una adaptación de la criba, con el cual 
generamos los números primos desde el 2 hasta el 100 mil. 





``` java
public class CribaEratostenes {
	
	//Mis observaciones
	//Cada 10 números naturales solamente puede haber como maximo 4 números primos 
	//Existen rangos de 10 numeros donde no existen números primos como por ejemplo
	//entre el 200 y el 210, que es el primero de los casos.
	//Tambien existe un patron de ceros que comienza en  101---103---107---109 y se repite 
	//Seguro tendra mucho que ver con la famosa función z 

	public static void main(String[] args) {
		primos();

	}

	public static void primos() {
		long principio, fin;
		principio = System.currentTimeMillis();

		//Creamos una lista
		List<Integer> lista = new ArrayList<Integer>();
		int desde = 2;
		int hasta = 99999;

		//rellenamos la lista con todos los numeros desde el 2 hasta el 100 mil
		for (int i = 0; i < hasta; i++) {
			lista.add(desde);
			desde++;
		}

		//implementamos la criba de Eratóstenes en java
		int siguienteEnLista = 1;
		for (int j = 0; j < lista.size(); j++) {
			for (int z = siguienteEnLista; z < lista.size(); z++) {
				
				if (lista.get(z) % lista.get(j) == 0) {
					lista.remove(z);
				}
			}
			siguienteEnLista++;
		}

		//guardamos el tiempo que tardo en ejecutar el algoritmo
		//para futuras mejoras de performance
		fin = System.currentTimeMillis();
		System.out.println((fin - principio)+ " milisegundos");

		int seleccionar = 10;
		//recorremos la lista de numeros primos y los imprimimos por consola
		for (int a = 0; a < lista.size(); a++) {
			
			
			if (lista.get(a)>seleccionar) {
				System.out.println();
				seleccionar+=10;
			    if(seleccionar<lista.get(a)){
				seleccionar+=10;
			    }
			}
			System.out.print(lista.get(a) + "-");
		}

	}

}


```

### Entendiendo el código

Vamos a lo que nos interesa, lo primero que hacemos es declarar un método donde implementaremos toda la lógica del algoritmo, luego creamos una lista que sera la que contendrá en principio todos los posibles números primos, luego llenamos la lista con dichos números, ahora viene la parte interesante, creamos un bucle for con el cual vamos a recorrer 
todos los elementos de la lista pero tomando el primer elemento de la lista vamos a entrar en otro bucle for (anidado)
con cual vamos a eliminar todos los múltiplos de dicho numero en el primer caso todos los múltiplos de dos, luego tomamos el segundo elemento de lista (3) con el cual hacemos los mismo y eliminamos todos sus múltiplos y así sucesivamente hasta
recorrer toda la lista, bastante simple, ahora ya tenemos nuestra lista cargada con todos los números primos en el rango 
solicitado, ahora lo que hacemos es imprimirlos, pero se me ocurrió que seria una buena idea imprimirlos ordenados por rangos de 10, osea los primos entre 1 y 10 luego entre 10 y 20 con lo cual me di cuenta de que en ciertos rango no existen
números primos, pero eso ya es un tema aparte y lo dejaremos para otra entrada.


>Todo el misterio que rodea a los números primos es mas que interesante y seguro sera motivo de próximas entradas en este blog.