# Crates-Buenox
# Rust Queue Implementation

This is an example of implementing a queue in Rust using `std::collections::VecDeque`. The queue allows you to add and remove items, as well as display relevant information about their current status.

## Features

- **Add a value to the queue:** Allows the user to add a value to the queue.
- **Remove a value from the queue:** Removes the first value from the queue.
- **Show first value:** Displays the first value in the queue.
- **Show Queue Length:** Shows the current length of the queue.
- **Show Queue Values:** Displays all values ​​present in the queue.

## Execution
Make sure you have Rust installed on your system. To compile and run the code, use the following command in your terminal:

```bash
cargo run

Here was used this crate :  https://crates.io/crates/dummy-queue
///
use std::collections::VecDeque;
use std::fmt::Debug;
use std::io::{self, Write};

struct Queue<T> {
    queue: VecDeque<T>,
}

impl<T: Debug> Queue<T> {
    fn new() -> Queue<T> {
        Queue { queue: VecDeque::new() }
    }

    fn enqueue(&mut self, item: T) {
        self.queue.push_back(item);
    }

    fn dequeue(&mut self) -> Option<T> {
        self.queue.pop_front()
    }

    fn front(&self) -> Option<&T> {
        self.queue.front()
    }

    fn len(&self) -> usize {
        self.queue.len()
    }

    fn is_empty(&self) -> bool {
        self.queue.is_empty()
    }

    fn to_string(&self) -> String {
        format!("{:?}", self.queue)
    }
}

pub fn run_cli() {
    let mut queue = Queue::<i32>::new();

    loop {
        println!("Menu:");
        println!("1. agregar un valor a la cola");
        println!("2. quitar un valor de la cola");
        println!("3. mostrar primer valor");
        println!("4. mostrar longitud de la cola");
        println!("5. mostrar los valores de la cola");
        println!("6. salir");

        let mut choice = String::new();
        print!("ingresa una opcion: ");
        io::stdout().flush().unwrap();
        io::stdin().read_line(&mut choice).unwrap();
        let choice: u32 = match choice.trim().parse() {
            Ok(num) => num,
            Err(_) => {
                println!("valor invalido oirfavor ingresa un numero valido.");
                continue;
            }
        };

        match choice {
            1 => {
                let mut input = String::new();
                print!("ingresa un valor a la cola: ");
                io::stdout().flush().unwrap();
                io::stdin().read_line(&mut input).unwrap();
                let value: i32 = match input.trim().parse() {
                    Ok(num) => num,
                    Err(_) => {
                        println!("Lo ingresado es invalido, porfavor ingresa un numero");
                        continue;
                    }
                };
                queue.enqueue(value);
            }
            2 => {
                if let Some(value) = queue.dequeue() {
                    println!("Deencolado: {}", value);
                } else {
                    println!("la cola esta vacia.");
                }
            }
            3 => {
                if let Some(value) = queue.front() {
                    println!("primero en cola: {}", value);
                } else {
                    println!("la cola esta vacia.");
                }
            }
            4 => {
                println!("la longitud de la cola es: {}", queue.len());
            }
            5 => {
                println!("la cola contiene: {}", queue.to_string());
            }
            6 => {
                println!("saliendo...");
                break;
            }
            _ => {
                println!("opcion invalida intente de nuevo porfa.");
            }
        }
    }
}


#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_works() {
        run_cli();
    }
}
