# Ejemplo de Multi-Hilos

Multi-hilos es una técnica que permite correr concurrentemente dos o mas partes de un programa, maximizando la utilización del CPU. Cada parte es llamada *hilo*.

Hay dos formas de crear aplicaciones multi-hilos en Java:

## Forma 1: Extendiendo de la clase *Thread*

### Constructores de la clase Thread

1. Thread( )
2. Thread(*String str*)
3. Thread(*Runnable r*)
4. Thread(*Runnable r*, *String str*)

### Métodos:

| Método        | **D**escripción                          |
| ------------- | ---------------------------------------- |
| setName()     | Asignarle un nombre al hilo              |
| getName()     | Obtener el nombre del hilo               |
| getPriority() | Retornar la prioridad del hilo           |
| isAlive()     | Verificar si el hilo aun esta activo     |
| join()        | Esperar que el hilo termine              |
| run()         | Punto de entrada al Hilo                 |
| sleep()       | Dormir el hilo por un tiempo definido    |
| start()       | Empezar el hilo llamando al método run() |

### Ejemplo

#### Archivo *ExtendedExample.java*

```java
package cr.una.multithread;

public class ExtendExample extends Thread {

    public ExtendExample(String name) {
        super(name);
    }

    public void run()
    {
        try
        {
            // Displaying the thread that is running
            System.out.println ("El hilo Extend con el NOMBRE [ " +
                    getName() + " ] y con el ID [ " + Thread.currentThread().getId() +
                    " ] esta corriendo");

        }
        catch (Exception e)
        {
            // Throwing an exception
            System.out.println ("Hubo una Excepción");
        }
    }
}

```

- Este ejemplo lo que hace es mostrar en la consola el nombre del hilo y el ID en donde esta corriendo.

## Forma 2: Implementando de la interfaz *Runnable*

### Ejemplo

#### Archivo *ImplementExample.java*

```java
package cr.una.multithread;

public class ImplementExample implements Runnable {
    public String name;

    public ImplementExample(String name) {
        this.name = name;
    }

    @Override
    public void run() {
        Thread.currentThread().setName(getName());
        try
        {
            // Displaying the thread that is running
            System.out.println ("El hilo Implement con el NOMBRE [ " +
                    Thread.currentThread().getName() + " ] y con el ID [ " + Thread.currentThread().getId() +
                    " ] esta corriendo");

        }
        catch (Exception e)
        {
            // Throwing an exception
            System.out.println ("Hubo una Excepción");
        }
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

}

```

- Este ejemplo lo que hace es mostrar en la consola el nombre del hilo y el ID en donde esta corriendo.

## Corriendo la aplicación

### Archivo *ThreadMainExample.java*

```java
import cr.una.multithread.ExtendExample;
import cr.una.multithread.ImplementExample;

public class ThreadMainExample {

    static void TestExtendExample() {
        ExtendExample extendExample1 = new ExtendExample("T1");
        ExtendExample extendExample2 = new ExtendExample("T2");
        ExtendExample extendExample3 = new ExtendExample("T3");
        ExtendExample extendExample4 = new ExtendExample("T4");

        extendExample1.start();
        extendExample2.start();
        extendExample3.start();
        extendExample4.start();
    }

    static void TestImplementExample() {
        Thread implementExample1 = new Thread(new ImplementExample("T1"));
        Thread implementExample2 = new Thread(new ImplementExample("T1"));
        Thread implementExample3 = new Thread(new ImplementExample("T1"));
        Thread implementExample4 = new Thread(new ImplementExample("T1"));

        implementExample1.start();
        implementExample2.start();
        implementExample3.start();
        implementExample4.start();
    }

    // Main Class
    public static void main(String[] args)
    {
        TestExtendExample ();
    }
}
```

- Este es el archivo *main*
- Hay dos métodos que diferencian las dos formas de correr hilos.
  - Al extender simplemente se instancia la clase y se inicia con el método start();
  - Al implementar se tiene que hacer una nueva instancia de la interfaz *thread* para poder utilizar el método start();