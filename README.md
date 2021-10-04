#include <stddef.h>
#include <stdio.h>
#include <stdlib.h>


typedef struct Node{   
    int id; 
    char *name;

    struct Node *next;  // создаем указатель на след. узел списка
} List; 

List *create(int set_id, char *set_name) {
    
    List *tmp = (List*)malloc(sizeof(List));// выделение памяти под корень списка
    
    tmp -> id = set_id; // присваивание значения узлу
    tmp -> name = set_name;
    tmp -> next = NULL;
    
    return tmp; // возвращаю значение
}
    
//добавление элемента в начале списка
void push_front(List **list, int set_id, char *set_name){ //новый узел
    
    List *new_element = create(set_id, set_name); 
    
    new_element -> next = *list;// переопределяю указатель на новый элемент
    *list = new_element;// новый элемент становится самым первым в списке
}

// добавление элемента в конец списка
void push_back(List **list, int set_id, char *set_name){ //новый узел
    
    List *new_element = create(set_id, set_name); 
    
    List *tmp = *list;
   
    while(tmp -> next != NULL) { // сдвиг копии указателя списка в самый конец первоначального списка
        tmp = tmp -> next;
    }
    tmp -> next = new_element;
    // присваивание указателю tmp -> next значения созданного нового узла
    // переопределяю переменную next в последнем элементе связного списка
}

// метод добавления нового элемента между элементом insert_id и следующим элементом
void insert_element(List **list, int insert_id, int set_id, char *set_name) { 
    
    List *tmp = *list;// объявляю новый указатель-копию списка list
    while (tmp -> next != NULL)// итерация списка
    {
        
        if (tmp -> id == insert_id)// останавливаюсь на элементе insert_id
        {
            
            List *new_element = create(set_id, set_name);// создаю новый элемент
       
            // теперь новый элемент указывает на элемент , следующий за insert_id, на который insert_id раньше указывал
            new_element -> next = tmp -> next;
            // изменяет указатель next элемента insert_id на новый элемент
            tmp -> next = new_element;
        }
        // прохожусь по всем элементам списка
        tmp = tmp -> next;
    }
}
int main()
{
	List *list = create(0,"Bogdan");
    
    push_front(&list, -1, "VLAD");
    push_front(&list, -2, "NIKITA");
    push_back(&list, 1, "GLEB");
    push_back(&list, 2, "DIMA");
	
	List *tmp=list;
	while(tmp->next !=NULL)
	{
		if(tmp->id==1){
			List *new_element=create(1000,"INSERT");
			new_element->next=tmp->next;
			tmp->next=new_element;
		}
		tmp=tmp->next;
	}
	
	
	
	
	while (list !=NULL){
	
	printf("id=%d name=%s\n", list->id, list->name);
	
		list=list -> next;
	}	
return 0;
}
