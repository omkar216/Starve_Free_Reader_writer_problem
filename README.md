# Starve_Free_Reader_Writer_Problem
Possible solution for the starve free Reader-Writer problem

## Starve Free Solution

A classical Reader Writer problem is a situation where multiple processes can access and modify a
shared ﬁle or data structure concurrently. In such a situation in order to avoid the race condition
only one writer should be allowed to access the critical section in any point of time and also when no
writer is active any number of reader can access the critical section. So to solve this synchronization
problem Binary Semaphores are used to lock and release the processes.







    //pseudo code for Starve Free solution

    binary_semaphore* s1= new binary_semaphore(1);

    binary_semaphore* s2= new binary_semaphore(1);

    static int reader_count=0;
    
    void down(binary_semaphore* s)
    {
       int  k= *s;
       if(k<=0) while(true); //TRAP
       k--;
       *s=k;
    
    }
    
     void up(binary_semaphore* s)
    {
       int  k= *s;
       if(k>=1) while(true); //TRAP
       k++;
       *s=k;
    
    }

    void reader( ) 
    {

        while(true){

        down( s1 );
        reader_count++;
        if(reader_count==1) then down( s2 );
        up( s1 );

        //HERE reader enter the critical section.

        down ( s1 );
        reader_count--;
        if(reader_count == 0) up( s2 );
        up( s1 );


      }

    }  

    void writer(  )
    {

        while(true){
        up( s2 );

         //HERE writer will enter the critical section.

        down( s2 );

      }
    } 
    
    
  

