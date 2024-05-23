# DLList.h

```c++
    #include <utility>
#include <iostream>

template <typename Object>
class DLList {
private:
struct N {
Object data;
N *prev;
N *next;

N(const Object &d = Object{}, N *p = nullptr, N *n = nullptr);
N(Object &&d, N *p = nullptr, N *n = nullptr);
};

public:
class const_iterator{
public:
const_iterator();
const Object &operator*() const;
const_iterator &operator++();
const_iterator operator++ (int);
bool operator== (const const_iterator& rhs) const;
bool operator!= (const const_iterator& rhs) const;

protected:
N* current;
Object& retrieve() const;
const_iterator(N *p);

friend class DLList<Object>;
};

class iterator : public const_iterator {
public:
iterator();
Object& operator*();
const Object& operator*() const;
iterator & operator++ ();
iterator &operator--();
iterator operator++ (int);
iterator operator-- (int);
iterator operator+ (int steps) const;

protected:
iterator(N *p);

friend class DLList<Object>;
};

public:
DLList();
DLList(std::initializer_list<Object> initList);
~DLList();
DLList(const DLList &rhs);
DLList &operator=(const DLList &rhs);
DLList(DLList &&rhs);
DLList &operator=(DLList &&rhs);

iterator begin();
const_iterator begin() const;
iterator end();
const_iterator end() const;

int size() const;
bool empty() const;

void clear();

Object &front();
const Object &front() const;
Object &back();
const Object &back() const;

void push_front(const Object &x);
void push_front(Object &&x);
void push_back(const Object &x);
void push_back(Object &&x);

void pop_front();
void pop_back();

iterator insert(iterator itr, const Object &x);
iterator insert(iterator itr, Object &&x);

void insert(int pos, const Object &x);
void insert(int pos, Object &x);

iterator erase(iterator itr);
void erase(int pos);
iterator erase(iterator from, iterator to);

void print() const;

private:
int theSize;
N *head;
N *tail;

void init();
iterator get_iterator(int pos);
};

#include "DLList.cpp"
```
###### El primer bloque de código es el siguiente

```c++
    template <typename Object>//plantillas
class DLList {//inicio de la clase 
```

###### En el anterior bloque de código  se puede ver como usan una plantilla (“template”) el cual sirve para poder manejar cualquier tipo de datos ya sea int, double, float entre otros y también se puede ver que si inicia la clase llamada DLList.

```c++
private:
    //definicion de la estructura de nodo
    struct N {
        Object data; //dato que se almacena en el nodo
        N *prev;//puntero a un nodo anterior
        N *next;//puntero al nodo que siqu
        //constructor de la estructura del nodo 
        N(const Object &d = Object{}, N *p = nullptr, N *n = nullptr);
        N(Object &&d, N *p = nullptr, N *n = nullptr);
};

```

###### Tenemos el private que determina que lo que sigue es privado  y no se puede acceder si no está dentro de la misma clase, se define una estructura llamada struct node que sirve para representar los nodos de la lista todos los nodos contiene un objeto llamado data y un puntero que apunta al nodo anterior y otro puntero que apunta al nodo siguiente llamados prev y next.

```c++
public:
class const_iterator{
public:
const_iterator();//constructor
const Object &operator*() const;//sobrecarga de desreferenciacion
const_iterator &operator++();//sobrecarga pre incremento
const_iterator operator++ (int);//sobrecarga post incremento
bool operator== (const const_iterator& rhs) const;//sobrecarga de igualdad
bool operator!= (const const_iterator& rhs) const;//sobrecarga de desigualdad

protected:
N* current;//puntero nodo
Object& retrieve() const;//datos del nodo
const_iterator(N *p);//constructor y puntero nodo

friend class DLList<Object>;//la clase DLList puede entrar protected

};

```

###### Clase de iteradores constantes que a grandes rasgos es para que defina iteradores constantes para recorrer una lista esta clase sobrecarga los operadores de diferentes maneras por ejemplo para el preincremento o para la igualdad entre otras también en modo protegido tiene un puntero que apunta al nodo actual una función que obtiene los datos del nodo y un constructor con un puntero al nodo hizo amiga a una clase para que pudiera entrar al la parte protegida y esa clase es la DLList.

```c++
class iterator : public const_iterator {
public:
iterator();//CONSTRUCTOR
Object& operator*();//sobrecarga desreferencia
const Object& operator*() const;//sobrecarga desreferencia iterador constante
iterator & operator++ ();//sobrecarga pre incremento
iterator &operator--();//sobrecarga pre decremento
iterator operator++ (int);//sobrecarga post incremento
iterator operator-- (int);//sobrecarca post decremento
iterator operator+ (int steps) const;//sobrecarga suma 

protected:
iterator(N *p);//constructor puntero nodo

friend class DLList<Object>;//permite accesoa a la clase DLList
};

```

###### Clase de iteración esta clase hereda la clase de iteración constante y se encarga de definir las iteraciones no constantes para el recorrido de las listas esta clase tiene su constructor y varias sobrecargas de operadores que se encargan de desreferencia, desreferencia de iteración constante, pre incremento y decremento, post incremento y decremento y  de la suma en modo protegido tiene un constructor con un puntero hacia el nodo y hace amigo  a otra clase para que pueda acceder lo que esté protegido a la clase que hizo amigo es a la DLList.

```c++
public:
DLList();//constructor
DLList(std::initializer_list<Object> initList);//constructor inicializador
~DLList();//destructor
DLList(const DLList &rhs);//constructor  copia
DLList &operator=(const DLList &rhs);//asignacion de copia 
DLList(DLList &&rhs);//constructor de movimiento
DLList &operator=(DLList &&rhs);//asignacion por movimiento
//iterador de inicio de la lista
iterator begin();
const_iterator begin() const;
//iterador de final de la lista 
iterator end();
const_iterator end() const;

int size() const;//metodo obtener tamaño de la lista
bool empty() const;//metodo de verificacion para saber si esta vacio

void clear();metodo para lipiar la lista 

//metodo para acceder al primer elemento de la lista
Object &front();
const Object &front() const;
//metodo para acceder al ultimo elemento de la lista 
Object &back();
const Object &back() const;

//metodo para agregar elementos al prinsipio de la lista
void push_front(const Object &x);
void push_front(Object &&x);
//metodo para agregar elemetos al final de la lista 
void push_back(const Object &x);
void push_back(Object &&x);

//metodo eliomina elemento de el inicio de la lista
void pop_front();
//elimina elemento final de la lista
void pop_back();

//puedes insertar elemetos en una uvicacion mas especifica de la lista 
iterator insert(iterator itr, const Object &x);
iterator insert(iterator itr, Object &&x);
void insert(int pos, const Object &x);
void insert(int pos, Object &x);

//elimina el elemento apuntado 
iterator erase(iterator itr);
//elimina el elemento en una posicion 
void erase(int pos);
//elimina los elementos de un rango
iterator erase(iterator from, iterator to);

//metodo para imprimir la lista 
void print() const;

```

###### Todo lo anterior son métodos, constructores, destructores y operadores públicos de la clase DLList.

```c++
private:
int theSize;// tammaño de la lista
N *head;//puntero al primer nodo
N *tail;//puntero al ultimo nodo

//funcion para inicializar la lista
void init();
//funcion iterador o pocicion exacta de la lista 
iterator get_iterator(int pos);
};
//inclucion del archivo DLList.cpp 
#include "DLList.cpp"
```
# DLList.cpp
```c++
#include "DLList.h"

template<typename Object>
DLList<Object>::N::N(const Object &d, N *p, N *n)
        : data{d}, prev{p}, next{n} {}

template<typename Object>
DLList<Object>::N::N(Object &&d, N *p, N *n)
        : data{std::move(d)}, prev{p}, next{n} {}

template<typename Object>
DLList<Object>::const_iterator::const_iterator() : current{nullptr} {}

template<typename Object>
const Object &DLList<Object>::const_iterator::operator*() const {
    return retrieve();
}

template<typename Object>
typename DLList<Object>::const_iterator &DLList<Object>::const_iterator::operator++() {
    current = current->next;
    return *this;
}

template<typename Object>
typename DLList<Object>::const_iterator DLList<Object>::const_iterator::operator++(int) {
    const_iterator old = *this;
    ++(*this);
    return old;
}

template<typename Object>
bool DLList<Object>::const_iterator::operator==(const const_iterator &rhs) const {
    return current == rhs.current;
}

template<typename Object>
bool DLList<Object>::const_iterator::operator!=(const const_iterator &rhs) const {
    return !(*this == rhs);
}

template<typename Object>
Object &DLList<Object>::const_iterator::retrieve() const {
    return current->data;
}

template<typename Object>
DLList<Object>::const_iterator::const_iterator(N *p) : current{p} {}

template<typename Object>
DLList<Object>::iterator::iterator() {}

template<typename Object>
Object &DLList<Object>::iterator::operator*() {
    return const_iterator::retrieve();
}

template<typename Object>
const Object &DLList<Object>::iterator::operator*() const {
    return const_iterator::operator*();
}

template<typename Object>
typename DLList<Object>::iterator &DLList<Object>::iterator::operator++() {
    this->current = this->current->next;
    return *this;
}

template<typename Object>
typename DLList<Object>::iterator &DLList<Object>::iterator::operator--() {
    this->current = this->current->prev;
    return *this;
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::iterator::operator++(int) {
    iterator old = *this;
    ++(*this);
    return old;
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::iterator::operator--(int) {
    iterator old = *this;
    --(*this);
    return old;
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::iterator::operator+(int steps) const {
    iterator new_itr = *this;
    for(int i = 0; i < steps; ++i) {
        ++new_itr;
    }
    return new_itr;
}

template<typename Object>
DLList<Object>::iterator::iterator(N *p) : const_iterator{p} {}

template<typename Object>
DLList<Object>::DLList() : theSize{0}, head{new N}, tail{new N} {
    head->next = tail;
    tail->prev = head;
}

template<typename Object>
DLList<Object>::DLList(std::initializer_list<Object> initList) : DLList() {
    for(const auto &item : initList) {
        push_back(item);
    }
}

template<typename Object>
DLList<Object>::~DLList() {
    clear();
    delete head;
    delete tail;
}

template<typename Object>
DLList<Object>::DLList(const DLList &rhs) : DLList() {
    for(auto &item : rhs) {
        push_back(item);
    }
}

template<typename Object>
DLList<Object> &DLList<Object>::operator=(const DLList &rhs) {
    DLList copy = rhs;
    std::swap(*this, copy);
    return *this;
}

template<typename Object>
DLList<Object>::DLList(DLList &&rhs) : theSize{rhs.theSize}, head{rhs.head}, tail{rhs.tail} {
    rhs.theSize = 0;
    rhs.head = nullptr;
    rhs.tail = nullptr;
}

template<typename Object>
DLList<Object> &DLList<Object>::operator=(DLList &&rhs) {
    std::swap(theSize, rhs.theSize);
    std::swap(head, rhs.head);
    std::swap(tail, rhs.tail);
    return *this;
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::begin() {
    return {head->next};
}

template<typename Object>
typename DLList<Object>::const_iterator DLList<Object>::begin() const {
    return {head->next};
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::end() {
    return {tail};
}

template<typename Object>
typename DLList<Object>::const_iterator DLList<Object>::end() const {
    return {tail};
}

template<typename Object>
int DLList<Object>::size() const {
    return theSize;
}

template<typename Object>
bool DLList<Object>::empty() const {
    return size() == 0;
}

template<typename Object>
void DLList<Object>::clear() {
    while(!empty()) {
        pop_front();
    }
}

template<typename Object>
Object &DLList<Object>::front() {
    return *begin();
}

template<typename Object>
const Object &DLList<Object>::front() const {
    return *begin();
}

template<typename Object>
Object &DLList<Object>::back() {
    return *(--end());
}

template<typename Object>
const Object &DLList<Object>::back() const {
    return *(--end());
}

template<typename Object>
void DLList<Object>::push_front(const Object &x) {
    insert(begin(), x);
}

template<typename Object>
void DLList<Object>::push_front(Object &&x) {
    insert(begin(), std::move(x));
}

template<typename Object>
void DLList<Object>::push_back(const Object &x) {
    insert(end(), x);
}

template<typename Object>
void DLList<Object>::push_back(Object &&x) {
    insert(end(), std::move(x));
}

template<typename Object>
void DLList<Object>::pop_front() {
    erase(begin());
}

template<typename Object>
void DLList<Object>::pop_back() {
    erase(--end());
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::insert(iterator itr, const Object &x) {
    N *p = itr.current;
    theSize++;
    return {p->prev = p->prev->next = new N{x, p->prev, p}};
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::insert(iterator itr, Object &&x) {
    N *p = itr.current;
    theSize++;
    return {p->prev = p->prev->next = new N{std::move(x), p->prev, p}};
}

template<typename Object>
void DLList<Object>::insert(int pos, const Object &x) {
    insert(get_iterator(pos), x);
}

template<typename Object>
void DLList<Object>::insert(int pos, Object &&x) {
    insert(get_iterator(pos), std::move(x));
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::erase(iterator itr) {
    N *p = itr.current;
    iterator retVal(p->next);
    p->prev->next = p->next;
    p->next->prev = p->prev;
    delete p;
    theSize--;
    return retVal;
}

template<typename Object>
void DLList<Object>::erase(int pos) {
    erase(get_iterator(pos));
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::erase(iterator from, iterator to) {
    for(iterator itr = from; itr != to;) {
        itr = erase(itr);
    }
    return to;
}

template<typename Object>
void DLList<Object>::print() const {
    for(const auto &item : *this) {
        std::cout << item << " ";
    }
    std::cout << std::endl;
}

template<typename Object>
void DLList<Object>::init() {
    theSize = 0;
    head = new N;
    tail = new N;
    head->next = tail;
    tail->prev = head;
}

template<typename Object>
typename DLList<Object>::iterator DLList<Object>::get_iterator(int pos) {
    iterator itr = begin();
    for(int i = 0; i < pos; ++i) {
        ++itr;
    }
    return itr;
}
```
```c++
#include "DLList.h"//icluir el aechivo  GLList.h

```
```c++
//implementacion del constructor node y punter previo y siguiente 
template<typename Object>
DLList<Object>::N::N(const Object &d, N *p, N *n)
        : data{d}, prev{p}, next{n} {}
```

###### Tenemos que esta implementación es una plantilla donde object es un tipo de dato genérico también se puede ver  que el constructor que se está implementando es de la clase interna N de la clase DLList, el constructor usa tres parámetros los cuales los cuales en orden serían una referencia constante a un objeto de tipo object  que es el dato que se almacenará en este nodo. puntero al nodo anterior de la lista  y un puntero al nodo siguiente de la lista. Tenemos la lista de inicialización del constructor data prev y next que en ese mismo orden su función es iniciar data con valor de d, iniciar prev con valor de p con un parámetro que apunta al nodo anterior y iniciar next con valor de n  con parámetro que apunta al siguiente nodo.

```c++
// Implementación del constructor N con dato movido y punteros previo y siguiente
template<typename Object>
DLList<Object>::N::N(Object &&d, N *p, N *n)
        : data{std::move(d)}, prev{p}, next{n} {}

```

###### Es muy parecida a la anterior pero un parámetro es diferente  en este caso es object &&d, esto indica que representa el dato que se moverá al nodo y en la inicialización lo que es diferente es que esta usado move para mover el dato d al miembro de datos.

```c++
// Implementación del constructor iterador constante
template<typename Object>
DLList<Object>::const_iterator::const_iterator() : current{nullptr} {}
```

###### Este también es una plantilla, el constructor que está implementando es de la clase iterador constante dentro de la clase 	DLLis y curren es un puntero  al nodo actual al que señala al iterador.

```c++
//implementacion desreferencia del iterador constante 
template<typename Object>
const Object &DLList<Object>::const_iterator::operator*() const {
    return retrieve();
}
```
###### Empezamos con la plantilla, el operador de desreferenciación pertenece a la clase iterador constante dentro de la clase DLList el operador no modifica el estado del objeto a el que se está apuntado el iterador y esto gracias a él const también se llama a la función retrieve que devuelve la referencia constante a el dato almacenado y se usa para acceder a los datos al que apunta el iterador.

```c++
// Implementación  de pre-incremento del iterador constante
template<typename Object>
typename DLList<Object>::const_iterator &DLList<Object>::const_iterator::operator++() {
    current = current->next;
    return *this;
}
```
###### Devuelve un objeto del iterador constante este operador se puede utilizar dentro de una expresión y luego continuar manipulando el mismo objeto el nodo se actualiza para apuntar al siguiente nodo de la lista y al final se devuelve una referencia a el iterador después de haber subido un nivel en la lista.

```c++
// Implementación de post-incremento del iterador constante
template<typename Object>
typename DLList<Object>::const_iterator DLList<Object>::const_iterator::operator++(int) {
    const_iterator old = *this;
    ++(*this);
    return old;
}
```

###### El retorno del operador es del iterador constante el parámetro int es un marcador para diferenciar este operador de preincremento, se crea una copia del iterador actual y se almacena en una variable llamada old se guarda la variable antes de que incremente, se devuelve la copia old.

```c++
// Implementación  de igualdad del iterador constante
template<typename Object>
bool DLList<Object>::const_iterator::operator==(const const_iterator &rhs) const {
    return current == rhs.current;
}
```

###### pertenece a la clase interna iterador constante este operador es un bool por lo que devuelve un valor de verdadero o falso que indicará en este caso si los iteradores son iguales o no son iguales, se tomará como referencia constante otro iterador  que representa el lado derecho de la comparación se compara el miembro current que es el nodo actual   a el iterador pasado.

```c++
// Implementación de desigualdad del iterador constante
template<typename Object>
bool DLList<Object>::const_iterator::operator!=(const const_iterator &rhs) const {
    return !(*this == rhs);
}
```

###### es muy parecido al anterior pero en vez de revisar si son iguales es lo contrario busca que sean distintos es decir si no son iguales el booleano regresa true a diferencia del anterior.

```c++
// Implementación de la función privada retrieve del iterador constante
template<typename Object>
Object &DLList<Object>::const_iterator::retrieve() const {
    return current->data;
}

```

###### Pertenece a la clase interna iterador constante es una función que está privada se implementa la función retrieve y devolverá una referencia a el dato almacenado en el nodo actual se puede acceder y modificar el dato almacenado en el nodo. 

```c++
// Implementación del constructor del iterador constante con un puntero a nodo
template<typename Object>
DLList<Object>::const_iterator::const_iterator(N *p) : current{p} {}

```

###### Este es el último que es de la clase interna del iterador constante toma un parámetro que es un puntero a un nodo y éste será el nodo a el que apuntar al inicio.

```c++
// Implementación del constructor del iterador
template<typename Object>
DLList<Object>::iterator::iterator() {}
```

###### Es el constructor del iterador que se encuentra dentro de la subclase iterador

```c++
// Implementación de desreferenciación del iterador
template<typename Object>
Object &DLList<Object>::iterator::operator*() {
return const_iterator::retrieve();
}
```

###### Pertenece a la clase interna iterador se llama la función retrieve del iterador constante para obtener una referencia a el objeto almacenado a el nodo que apunta el iterador, con la función retrieve  devuelve la referencia a el dato almacenado en el nodo para la desreferenciación.  

```c++
// Implementación de desreferenciación constante del iterador
template<typename Object>
const Object &DLList<Object>::iterator::operator*() const {
return const_iterator::operator*();
}
```

###### Esto es de la clase interna iterador se llama a el operador de desreferenciación de la clase iterador constante.

```c++
// Implementación de pre-incremento del iterador
template<typename Object>
typename DLList<Object>::iterator &DLList<Object>::iterator::operator++() {
    this->current = this->current->next;
    return *this;
}
```

###### Es de la  clase interna iterador indica que el operador devuelve una referencia al propio iterador después de la operación de incremento, se actualiza el puntero current del iterador al puntero next. Esto mueve el iterador al siguiente nodo en la lista y devuelve una  referencia al iterador después de haber incrementado.

```c++
// Implementación de pre-decremento del iterador
template<typename Object>
typename DLList<Object>::iterator &DLList<Object>::iterator::operator--() {
    this->current = this->current->prev;
    return *this;
}
```

###### Es prácticamente igual al anterior solo que en vez de aumentar uno en la lista de nodos va uno hacia abajo en la lista de nodos.

```c++
// Implementación del operador de post-incremento del iterador
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::iterator::operator++(int) {
    iterator old = *this;
    ++(*this);
    return old;
}
```

###### Es parte de la clase interna iterador este crea una copia del iterador actual y la guarda en una variable llamada old para proseguir incrementado un lugar en la lista y al final se devuelve el valor guardado en la variable old. 

```c++
// Implementación de post-decremento del iterador
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::iterator::operator--(int) {
    iterator old = *this;
    --(*this);
    return old;
}
```
###### Es practicamente igual a el bloque anterior de codigo solo que baja un lugar en la lista en vez de subirlo.

```c++
**// Implementación de suma del iterador
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::iterator::operator+(int steps) const {
    iterator new_itr = *this;
    for(int i = 0; i < steps; ++i) {
        ++new_itr;
    }
    return new_itr;
}**
```
###### Es una clase interna  iterador se creará una copia del iterador actual y se almacena en una variable llamada new_itr tiene un bucle for en el que por cada iteración se incrementa la variable new_itr y al final se devolverá el valor después de haber avanzado en la lista una cierta cantidad de pasos.

```c++
// Implementación del constructor del iterador con un puntero a nodo
template<typename Object>
DLList<Object>::iterator::iterator(N *p) : const_iterator{p} {}
```
###### Este es el último que es parte de la clase interna iterador se llama el constructor de la clase base iterador constante con el punto a el nodo p. 

```c++
// Implementación del constructor de DLList
template<typename Object>
DLList<Object>::DLList() : theSize{0}, head{new N}, tail{new N} {
    head->next = tail;
    tail->prev = head;
}
```
###### Se puede notar que este ya es directamente de la clase DLList se inicializa el tamaño de la lista  crea un nodo y asigna su dirección de memoria a el puntero y representará la cabeza de la lista y por último crea otro nuevo nodo y asigna su dirección a el puntero y representa la cola de la lista y se establece una conexión entre el primer nodo y el último y viceversa.

```c++
// Implementación del constructor de DLList con un inicializador de lista
template<typename Object>
DLList<Object>::DLList(std::initializer_list<Object> initList) : DLList() {
    for(const auto &item : initList) {
        push_back(item);
    }
}
```
###### Dentro del cuerpo del constructor se itera se itera sobre cada inicializador de lista usando un bucle for para cada elemento del inicializador de la lista se llama a el método y se insertará el elemento al final de la lista. 

```c++
// Implementación del destructor de DLList
template<typename Object>
DLList<Object>::~DLList() {
    clear();
    delete head;
    delete tail;
}
```
###### En este bloque de codigo se destuira lo que se creo en el constructor de DLList

```c++
// Implementación del constructor de copia de DLList
template<typename Object>
DLList<Object>::DLList(const DLList &rhs) : DLList() {
    for(auto &item : rhs) {
        push_back(item);
    }
}
```
######  Se llama el constructor por defecto se itera en cada elemento de la lista usando el bucle for y se inserta cada elemento de la lista que se está construyendo.

```c++
// Implementación del operador de asignación por copia de DLList
template<typename Object>
DLList<Object> &DLList<Object>::operator=(const DLList &rhs) {
    DLList copy = rhs;
    std::swap(*this, copy);
    return *this;
}
```
###### Se crea una copia  de lista rhs esto crea una lista temporal copy que es una copia exacta de rhs se intercambian los elementos de la lista actual  con los de la lista copy y se devuelve una referencia de la lista actual.

```c++

// Implementación del constructor de movimiento de DLList
template<typename Object>
DLList<Object>::DLList(DLList &&rhs) : theSize{rhs.theSize}, head{rhs.head}, tail{rhs.tail} {
rhs.theSize = 0;
rhs.head = nullptr;
rhs.tail = nullptr;
}
```

###### Se inicializan los miembros de datos thesize, head y tail con los valores de la instancia revalue que se encargan de copiar el tamaño de la lista, se copia el nodo de el principio y el del final respectivamente y al final se modifican los valores  de tamaño a 0 y el de la cabeza y cola al nullptr lo que significa a movido las propiedades de la lista y ya no se hace responsable de liberarlos. 

```c++
// Implementación del operador de asignación por movimiento de DLList
template<typename Object>
DLList<Object> &DLList<Object>::operator=(DLList &&rhs) {
    std::swap(theSize, rhs.theSize);
    std::swap(head, rhs.head);
    std::swap(tail, rhs.tail);
    return *this;
}
```
###### Se intercambiaran los valores de los miembros de datos entre la instancia actual y la instancia rvalue se intercambia el tamaño de la lista entre la instancia actual y la rvalue se intercambia también los punteros de los nodos cabeza y cola entre la instancia actual y la rvalue se devuelve la nueva instancia después de intercambiar los valores.

```c++
// Implementación del método begin para obtener el iterador de inicio de DLList
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::begin() {
    return {head->next};
}

```
###### Este método devuelve  un iterador que apunta al primer elemento de la lista.

```c++
// Implementación del método begin para obtener el iterador de inicio constante de DLList
template<typename Object>
typename DLList<Object>::const_iterator DLList<Object>::begin() const {
    return {head->next};
}
```
###### Es lo mismo que la anterior pero para la clase iterador constante.

```c++
// Implementación del método end para obtener el iterador de fin de DLList
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::end() {
    return {tail};
}
```
###### Este método devuelve un iterador que apunta a el último elemento de la lista para indicar que la lista ha terminado. 
```c++
// Implementación del método end para obtener el iterador de fin constante de DLList
template<typename Object>
typename DLList<Object>::const_iterator DLList<Object>::end() const {
    return {tail};
}
```
###### Es lo mismo que la anterior pero para la clase iterador constante.

```c++
// Implementación del método size
template<typename Object>
int DLList<Object>::size() const {
    return theSize;
}
```
###### En este metodo solo es para que se de a conozer el tamaño de la lista.

```c++
// Implementación del método vacío
template<typename Object>
bool DLList<Object>::empty() const {
    return size() == 0;
}
```
###### Este es un booleano que lo que busca es saber si el tamaño de la lista es 0 es verdadero y si no pues falso.

```c++
// Implementación del método clear
template<typename Object>
void DLList<Object>::clear() {
    while(!empty()) {
        pop_front();
    }
}
```
###### Es un bucle while que se ejecuta mientras que la lista no esté vacía llamado a la función empty para revisarlo y si no está vacía se ejecuta un método pop_front este método elimina el primer elemento de la lista  y el bucle se ejecutara hasta que se haya eliminado el último elemento de la lista.

```c++
// Implementación del método front
template<typename Object>
Object &DLList<Object>::front() {
    return *begin();
}
```

###### Este método regresa una referencia al primer elemento de la lista usando un puntero.

```c++
// Implementación del método front  el primer elemento constante de DLList
template<typename Object>
const Object &DLList<Object>::front() const {
    return *begin();
}
```

###### Es igual a el método anterior pero esta vez regresa un elemento constante inicial de la lista.

```c++
// Implementación del método back
template<typename Object>
Object &DLList<Object>::back() {
    return *(--end());
}
```

######  Devuelve  una referencia al último elemento de la lista usando un puntero.

```c++

// Implementación del método back último elemento constante de DLList
template<typename Object>
const Object &DLList<Object>::back() const {
    return *(--end());
}
```

###### Es igual a el método anterior pero esta vez regresa un elemento constante final de la lista.  

```c++
// Implementación del método push_front
template<typename Object>
void DLList<Object>::push_front(const Object &x) {
    insert(begin(), x);
}

```

###### utiliza el método insert para insertar el elemento x  al principio de la lista.

```c++
// Implementación del método push_front(moviendo)
template<typename Object>
void DLList<Object>::push_front(Object &&x) {
    insert(begin(), std::move(x));
}
```

###### Es casi igual al anterior solo que en este se usa move para mover el contenido del objeto x al nuevo elemento de la lista.

```c++
// Implementación del método push_back
template<typename Object>
void DLList<Object>::push_back(const Object &x) {
    insert(end(), x);
}
```

###### Usa la función inseri y end para insertar el elemento x al final de la lista.

```c++
// Implementación del método push_back(moviendo)
template<typename Object>
void DLList<Object>::push_back(Object &&x) {
    insert(end(), std::move(x));
}
```

###### Es casi igual al anterior solo que en este se usa move para mover el contenido del objeto x al nuevo elemento de la lista.

```c++
// Implementación del método pop_front
template<typename Object>
void DLList<Object>::pop_front() {
    erase(begin());
}
```
###### En este este método se usa la función erase y la función begin para borrar el primer elemento de la lista. 

```c++
// Implementación del método pop_back
template<typename Object>
void DLList<Object>::pop_back() {
    erase(--end());
}
```

###### Es igual al método anterior solo que en vez de la función begin usa la función end para borrar el último elemento de la lista.

```c++
// Implementación del método insert para insertar un elemento en una posición específica de DLList
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::insert(iterator itr, const Object &x) {
    N *p = itr.current;
    theSize++;
    return {p->prev = p->prev->next = new N{x, p->prev, p}};
}
```

###### Se obtiene un puntero al nodo al nodo que se le quiere insertar el nuevo elemento se incrementa el tamaño de la lista y se crea un nuevo nodo con el valor x se actualiz en los puntos prev y next de los nodos adyacentes se devuelve un iterador que apunta al nuevo elemento. 

```c++
// Implementación del método insert para insertar un elemento en una posición específica de DLList (moviendo)
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::insert(iterator itr, Object &&x) {
    N *p = itr.current;
    theSize++;
    return {p->prev = p->prev->next = new N{std::move(x), p->prev, p}};
```

###### Es prácticamente igual al anterior pero este tiene una función move para mover el recurso y no hacer copias.

```c++
// Implementación del método insert
template<typename Object>
void DLList<Object>::insert(int pos, const Object &x) {
    insert(get_iterator(pos), x);
}
```

###### Se llama al método insert se obtiene un iterador correspondiente a la posición que devuelve un iterador válido para la posición dada de la lista.

```c++
// Implementación del método insert (moviendo)
template<typename Object>
void DLList<Object>::insert(int pos, Object &&x) {
    insert(get_iterator(pos), std::move(x));
}
```

###### Es prácticamente igual a el método anterior pero es una una función move para hacer una transferencia de recursos del objeto x.

```c++
// Implementación del metodo erase
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::erase(iterator itr) {
    N *p = itr.current;
    iterator retVal(p->next);
    p->prev->next = p->next;
    p->next->prev = p->prev;
    delete p;
    theSize--;
    return retVal;
}
```

###### Se obtiene un puntero al nodo que se va a eliminar se crea un iterador retval que se apunta al nodo siguiente que se va a borrar se actualiza el puntero next y prev se elimina el nodo p se encoge el tamaño de la lista y se devuelve el iterador retvalue que apunta al nodo que sigue del que se eliminó. 

```c++
// Implementación del método erase para eliminar un elemento en una posición específica de DLList
template<typename Object>
void DLList<Object>::erase(int pos) {
    erase(get_iterator(pos));
}
```

###### Se llama el método erase se llama la funcion get iterator para conseguir la posición del iterador que se borrar y se borra.

```c++
// Implementación del método erase para eliminar un rango de elementos en DLList
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::erase(iterator from, iterator to) {
    for(iterator itr = from; itr != to;) {
        itr = erase(itr);
    }
    return to;
}
```

###### Este bucle for hace iteraciones desde from  hasta  to en cada iteración se llama al método erase y se va repitiendo hasta llegar a to y borra todos los elementos que hay en medio.

```c++
// Implementación del método print
template<typename Object>
void DLList<Object>::print() const {
    for(const auto &item : *this) {
        std::cout << item << " ";
    }
    std::cout << std::endl;
}
```

###### Tenemos un bucle for que itera a través de todos los elemento de la lista aplicándoles un cout para imprimir cada elemento de la lista.

```c++
// Implementación del método init
template<typename Object>
void DLList<Object>::init() {
    theSize = 0;
    head = new N;
    tail = new N;
    head->next = tail;
    tail->prev = head;
}
```

###### Inicializa el tamaño de la lista en 0, crean dos nuevos nodos que son el head y tail y se establece que head next =  tail y tail prev = head para apuntarse entre sí.

```c++
// Implementación del método get_iterator
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::get_iterator(int pos) {
    iterator itr = begin();
    for(int i = 0; i < pos; ++i) {
        ++itr;
    }
    return itr;
}
```

###### Crea un iterator  itr que apunta al primer elemento de la lista, tenemos un bucle for este bucle incrementa itr pos para avanzar las posiciones que se desean  y devuelve el iterator itr que apunta al elemento posición. 
