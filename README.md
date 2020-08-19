# osAssignement
#include<stdio.h>
#define MAX 20

void mergeSort(int arr[],int low,int mid,int high);

void partition(int arr[],int low,int high);

void quicksort(int [10],int,int);

void main()
{
    int a[10],i,n,x;

    printf(“\n ————————-“);
    printf(“Enter the no of element:”);
    scanf(“%d”,&n);

    printf(“enter the elements:”);
    for(i=0;i<n;i++)
    scanf(“%d”,&a[i]);

    x=fork();
    if(x==0)
    {
    printf(“\nchild process = %d”,getpid());

    quicksort(a,0,n-1);
    printf(“\nAfter quick sorting elements are: “);

    for(i=0;i<n;i++)
    printf(” %d”,a[i]);
    }
    else 
    {
    printf(“\nparent process=%d \n”,getpid());
    partition(a,0,n-1);
    printf(“\nAfter merge sorting elements are: “);
    for(i=0;i<n;i++)
    printf(“%d “,a[i]);
    }
}

void partition(int arr[],int low,int high)
{

    int mid;
    if(low<high)
    {
    mid=(low+high)/2;
    partition(arr,low,mid);
    partition(arr,mid+1,high);
    mergeSort(arr,low,mid,high);
    }
}

void mergeSort(int arr[],int low,int mid,int high)
{
    int i,m,k,l,temp[MAX];
    l=low;
    i=low;
    m=mid+1;
    while((l<=mid)&&(m<=high))
    {
    if(arr[l]<=arr[m])
    {
    temp[i]=arr[l];
    l++;
    }
    else
    {
    temp[i]=arr[m];
    m++;
    }
    i++;
    }
    if(l>mid)
    {
    for(k=m;k<=high;k++)
    {
    temp[i]=arr[k];
    i++;
    }
    }
    else
    {
    for(k=l;k<=mid;k++)
    {
    temp[i]=arr[k];
    i++;
    }
    }

    for(k=low;k<=high;k++)
    {
    arr[k]=temp[k];
    }
}

void quicksort(int x[10],int first,int last)
{
    int pivot,j,temp,i;
    if(first<last)
    {
    pivot=first;
    i=first;
    j=last;
    while(i<j)
    {
    while(x[i]<=x[pivot]&&i<last)
    i++;
    while(x[j]>x[pivot])
    j–;
    if(i<j)
    {
    temp=x[i];
    x[i]=x[j];
    x[j]=temp;
    }
    }
    temp=x[pivot];
    x[pivot]=x[j];
    x[j]=temp;
    quicksort(x,first,j-1);
    quicksort(x,j+1,last);
    }
#include <stdio.h> 
#include <stdlib.h> 
#include <unistd.h> 


int main() 
{ 
int pid, pid1, pid2; 

pid = fork(); 

if (pid == 0) { 

sleep(3); 

printf("child[1] --> pid = %d and ppid = %d\n", 
getpid(), getppid()); 
} 

else { 
pid1 = fork(); 
if (pid1 == 0) { 
sleep(2); 
printf("child[2] --> pid = %d and ppid = %d\n", 
getpid(), getppid()); 
} 
else { 
pid2 = fork(); 
if (pid2 == 0) { 
printf("child[3] --> pid = %d and ppid = %d\n", 
getpid(), getppid()); 
} 

else {  
sleep(3); 
printf("parent --> pid = %d\n", getpid()); 
} 
} 
} 

return 0; 
#include <stdio.h>

int main(){
    pid_t child_pid;
    child_pid=fork();
    if(child_pid==0){ 
        child_pid=fork();
        if(child_pid==0){ 
            child_pid=fork(); 
        }
    }
    else{ 
        child_pid= 0;
        child_pid=fork(); 
        if(child_pid==0){ 
            child_pid=fork(); 
            if(child_pid>0){
                fork();
            }
        }
#include <pthread.h>

#include <stdio.h>

#include <stdlib.h>

pthread_mutex_t mutex;

int fib[10]; 

int in = 0;

void *genFibo(void *param); 

int main(int argc, char *argv[])

{

   pthread_attr_t attr;  

   if (argc != 2) {

   fprintf(stderr,"usage: fibthread <integer value>\n");

   return -1;

   }

   int count = atoi(argv[1]);
   if (count < 1) {

   fprintf(stderr,"%d must be>= 1\n", count);

   return -1;

   }

   pthread_attr_init(&attr);

   pthread_mutex_init(&mutex, NULL);

   for(int i = 1;i <= count;i++) {

   pthread_t thread;

   pthread_create(&thread, &attr, genFibo, (void*)i);

   pthread_join(thread, NULL);    

   }    

   for (int i = 0; i < in;i++) {

   printf("%d ", fib[i]);

   }

   printf("\n");

   pthread_mutex_destroy(&mutex);

}

void *genFibo(void *param)

{

   pthread_mutex_lock(&mutex);

   fib[in++] = fibonacci((int)param);
   pthread_mutex_unlock(&mutex);

   pthread_exit(0);

}

int fibonacci (int x)

{

   if (x <= 1) {

   return 1;

   }

   return fibonacci(x-1) + fibonacci(x-2);

} 
    }
} -----
}-----
} ---
