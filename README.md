# operating
#include<stdio.h>
#include<stdlib.h>

void producer();
void consumer();
int wait(int);
int signal(int);
int mutex=1,full=0,empty=3,x=0;

int main(){
    int ch;
    printf("1.Producer\n2.Consumer\n3.Exit\n");
    while(1){
        printf("\nEnter your choice\n");
        scanf("%d",&ch);
        
        switch(ch)
        {
            case 1:if((mutex==1)&&(empty!=0))
            producer();
            else
            printf("Buffer is full");
            break;
            
            case 2:if((mutex==1)&&(full!=0))
            consumer();
            else
            printf("Buffer is empty");
            break;
            
            case 3:
            exit(0);
        }
        
    }
    return 0;
}

int wait(int s)
{
    return(--s);
}

int signal(int s)
{
    return(++s);
}

void producer()
{
    mutex=wait(mutex);
    full=signal(full);
    empty=wait(empty);
    x++;
    printf("producer produces items:%d",x);
    mutex=signal(mutex);
    
}

void consumer()
{
    mutex=wait(mutex);
    full=wait(full);
    empty=signal(empty);
   
    printf("consumer consumess items:%d",x);
     x--;
    mutex=signal(mutex);
    
}


