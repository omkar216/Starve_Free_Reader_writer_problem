# Starve_Free_Reader_Writer_Problem
Possible solution for the starve free Reader-Writer problem

## Starve Free Solution





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
    
    
  

