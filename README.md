# Testme123
// a web application maintains a list of usernames and must quickly determine whether a new username already exists 
// develop a c prgramm a to implement hashing for strong username .use a suitable hash function and collision resolution strategy and support operations such as insert and search ,

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define TABLE_SIZE 10

struct Node{
    char name[30];
    struct Node*next;

}
struct Nose*hashtable[TABLE_SIZE];
int hashFunction(char* name){
    int sum = 0;
    for(int i=0; name[i]!='\0'; i++){
        sum += name[i];
    }
    return sum % TABLE_SIZE;
}
void insert(char* name){
    int index = hashFunction(name);
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    strcpy(newNode->name, name);
    newNode->next = NULL;

    if(hashtable[index] == NULL){
        hashtable[index] = newNode;
    } else {
        struct Node* temp = hashtable[index];
        while(temp->next != NULL){
            temp = temp->next;
        }
        temp->next = newNode;
    }
    printf("Inserted username: %s\n", name);
}
int search(char* name){
    int index = hashFunction(name);
    struct Node* temp = hashtable[index];
    while(temp != NULL){
        if(strcmp(temp->name, name) == 0){
            return 1; // Found
        }
        temp = temp->next;
    }
    return 0; // Not found
}
int main(){
    // Initialize hashtable
    for(int i=0; i<TABLE_SIZE; i++){
        hashtable[i] = NULL;
    }

    insert("alice");
    insert("bob");
    insert("charlie");

    char username[30];
    printf("Enter username to search: ");
    scanf("%s", username);

    if(search(username)){
        printf("Username %s already exists.\n", username);
    } else {
        printf("Username %s is available.\n", username);
    }

    return 0;
}




ṇ
