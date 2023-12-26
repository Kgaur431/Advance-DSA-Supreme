### Introduction
``` 
    till now we have studied three sorting algorithm Bubble Sort, Selection Sort, Merge sort.
    In all the three sorting algorithm there was a conditon that 'we are given all the input at once' so we have the complete data & we have to arrange the data in the order.
    
    In real life sometimes we don't have the complete data at once.
    like:-
        sometimes we have some data right now that we arrange & some data comes letter on & that we have to fit in the arranged data. 
```

### we have to sort a running input stream for all integer intake. (basically one by one we get integers we have to make sure that data with us will remain in a sorted order) by default sorted order is ASC.
``` 
    I/p = 2
          2         //single element is already sorted.
          
    next I/P = 2 10
          2 10      // it is in correct order.

    next I/P = 2 10 8
          2 10      // now 8 is in the input, in Ascending order 8 will come before 10.
         
          let say, we are storing this data (2 10), becoz we don't aware how much data can come so we used Dynamic array. like ArrayList.
          
          Ques:-    In the Dynamic Array, Is it possible to insert the element in between (2 10) ?
          Ans :-    10 will shift one step right to make space for element 8. then we will insert an element 2 in between 2 10. img 2.
                    ex:-
                        there are some elements in the dynamic array, each array has particular index. if we try to insert the element 6 between at index 2. 
                        then where the element 3 will go. img 1. 
                        In that case all the element will move one step right.
                        
                    Ques:-  What is the TC to insert in between || shifting elements ?
                    Ans :-  O(N).  it will take linear time to shift every data into right.     

    next I/P = 2 10 8 7 
          2 8 10.
          so element 10 will be shifted to right then element 8 will shifted to right.
          then we place the element 7.
          2 7 8 10. 
    
    we are doing shifting & insert the element.
    
    Ques:-  What is the min no. of shift we need at any point ?             // important question 
    
    next I/P = 2 10 8 7 15
          2 7 8 10 15       here, we need 0 shifts.                     // min number of shifts.
    
    Ques:-  What is the max no. of shift we need ?                     // important question
    Ans :-  if we have total no. of k elements then maximum no. of shift is k.  O(N).
            no. of elements = no. of shifts.
    
    next I/P = 2 10 8 7 15 1
          1 2 7 8 10 15 
    
    If we have total no. of elements = N, then TC (What it the total time that we will take to shift for every intake) will be = O(N^2)  becoz for 1 element to shift it is taking O(N) then for N element it is taking O(N^2).
    
    Activity:-
        I/p = 9 8 3 1
        
        Ques:-  What is the maximum shift do we need 
        Ans :-  6
                elements        No. off shifts
                   9                0           we don't need to shift any thing if we have only 9 in the array.
                   8                1           now, in the array we have 9 8.  8<9 so we need to shift 9, one step right to make space for element 8. 
                   3                2           now, in the array we have 9 8 3.  3<8 9 so we need to shift 9 & 8 both, one - one step right to make space for element 3. 
                   1                3           now, in the array we have 9 8 3 1.  1<3 8 9 so we need to shift 9 8 & 3, one - one step right to make space for element 1.
                   .                .
                   .                .
                   .                N-1
                            -------------------------
                         total =    6  
                         it is nothing but sum of natural number till N-1.
                         = N*(N-1)/2
                         = N^2          it is also justify that TC = O(N^2).
    
    Insertion Sort:-    this algo is very important becoz it is the sorting algo that help us deal with the running integer. so if we don't have the complete input then this is the algo that we have to use.
                            if we have complete input then merge sort is the best algo. (insertion sort, selection sort, bubble sort)
    this is know as Insertion Sort.
    TC = O(N^2)
    SC = O(1)           // we don't need to shift using any extra space just use output array.
    
    Code:-
        int i;
        n=0         // initially we have 0 elements
        for (all input x)           it means, if we have the array (complete array) then run this for loop till complete array. like we are inserting the element one by one. so if we have four element this loop will work 4 timest. 
        {                           now, for every element we will see that how many elements are bigger than that element. like if element 6 we are inserting then we will see that how many elements are bigger than that element 6 that much we shift. 
            for(i=n; i>0; i--)      so run the loop in reverse order.
            {
                if(A[i-1] > x)      means if A[i-1] elements are greater than the current element we are inserting.
                {
                    A[i] = A[i-1];  then we update A[i] = A[i-1];
                }
                else 
                {
                    break;          means, if current element is not greater then no need to shift.
                }
            }
            
            A[i] = x;
            n += 1;
         }
    
    Dry run:-
             0 1 2 3  4
            [9 8 6 7 12]
                            for (all input x)   ==> we can consider it running queue of integers. when element come into the queue then the inner for loop will execute. like if 10 elements come then inner loop will execute 10 times.
            initially n=0 we don't have anything in the input. we have arraylist (purple color) {if we know what is the total no. of element we are going to get then use array}.
            first element (x) 9 come in the queue, for loop will start from i=0. becoz we have to place the element at i=0, here, i>0 condition is not true so the inner for loop will not work & we update A[i] = x now n=1(means we have element 9 
                at index 0).        means for the first element we no need to run inner loop we just store the first element at index 0.
            second element (x) 8 in the queue (x=8), i=1 (means we try to insert data at index 1) so i>0 means we are in inner for loop. now we check if element at index 0 is greater than current element then we copy the index 0 element to index 1. img 4. 
                then i-- means i=0, as soon as i=0 we come back from inner loop. & store the current element into index 0 & increase the n, n=2.
            third element (x) 6  in the queue, i=2 (means we try to insert data at index 2) so i>0 means we are in inner for loop. now we check if element at index 1 is greater than current element then we copy the index 1 element to index 2. img 5.
                then i-- means i=1, now we check if element at index 0 is greater than current element then we copy the index 0 element to index 1. img 6.
                now i=0 as soon as i=0 we come back from inner loop. & store the current element into index 0 & increase the n, n=3. means we have 3 element in the array. img 6.
            fourth element (x) 7  in the queue, i=3 (means we try to insert data at index 3) so i>0 means we are in inner for loop. now we check if element at index 2 is greater than current element then we copy the index 2 element to index 3. 
                then i-- means i=2, now we check if element at index 1 is greater than current element then we copy the index 1 element to index 2. 
                then i=1 now we check if element at index 0 is greater than current element yes then we come out from the loop. now we not shift.
                & store the current element into index 1 & increase the n, n=4. means we have 4 element in the array.
            fifth element (x) 12  in the queue, i=4 (means we try to insert data at index 4) so i>0 means we are in inner for loop. now we check if element at index 3 is greater than current element, No. & we execute the else part means break the loop & come ourt from the inner loop.
                & store the current element into index 4 & increase the n, n=5. means we have 4 element in the array.
            
            now , all the elements are in the sorted order.
            
    Real World Scanerio:-
        let say, we have a website where we are storing a users data, every data new users are coming so in that case Insertion Sort is very useful.
```

### Given N nuts of different size & N bolts of diff sizes. there is a 1:1 mapping between nuts & bolt (means one nut exactly matching with one bolt). our goal is to match nuts & bolts with an constraints that comparing a nut with itself & a bolt with itself is not allowed. when we compare a nut & a bolt then three things can happen.
1.  exactly fits.    
2.  nut is small.      (means nut is loose)
3.  nut is high.      (means nut is big, even it is not go into boult)
``` 
    we can't compare a nut with the nut || boult with the boult. we can compare a nut & a boult with the above three case.
    
    Bruteforce:-
        "Compare all nuts with all boults".
            like:-
                we first pick the boult Ba & compare with all the nuts. so we need 6 comparision for this.  let say, Ba boult fits with N5 nut. means we found the match.
                then we pick the boult Bb & compare with all the remaining 5 nuts. so we need 5 comparision for this.  let say, Bb boult fits with N1 nut. means we found the match.
                then we pick the boult Bc & compare with all the remaining 4 nuts. so we need 4 comparision for this.  let say, Bc boult fits with N4 nut. means we found the match.
                then we pick the boult Bd & compare with all the remaining 3 nuts. so we need 3 comparision for this.  let say, Bd boult fits with N6 nut. means we found the match.
                then we pick the boult Be & compare with all the remaining 2 nuts. so we need 2 comparision for this.  let say, Be boult fits with N3 nut. means we found the match.
                then we pick the boult Bf & compare with all the remaining 1 nuts. so we need 1 comparision for this.  let say, Bf boult fits with N2 nut. means we found the match.
                
                so the no. of comparision is:- 6 + 5 + 4 + 3 + 2 + 1 = 21 comparision we need if we have 6 nuts & boult.
               
                What is the TC we need for N nuts & boults ?
                TC = O(N^2).    for 1 boult we are comparing with N nuts, so for n nut we will will compare with N-1 boult. N * N-1 = N^2.
    Concept ?:- 
                
        let say, we picked any randdom boult like Ba & we compare Ba with every nut like N1, let say N1 nut is smaller (loose) for this boult Ba, so we arrange one table, on one side of table we kept which are smaller.
        now we compare with N2, it also small so we kepted on the smaller side of the table. we compare with N3, it bigger so we kepted on the other side of the table. we compare with N4, it also small so we kepted on the smaller side of the table.
        we compare with N5, it fits (matched), it's random decision, we compare with N6, even we already matched but we just compare it, it bigger so we kepted on the bigger side of the table.  img 8.
            left side of the table where nuts are small,        nuts are fixed size,        right side of the table where nuts are bigger 
                                                                N5 are match with Ba
        
        let say, now we picked boult Bb & the Bb boult was smaller for the nut N5 so we kept the Bb boult on the left side of the table(where small nuts are there). 
        Bc boult are bigger for the nut N5 so we kept the Bc boult on the right side of the table(where bigger nuts are there),
        Bd boult are smaller for the nut N5 so we kept the Bd boult on the left side of the table(where smaller nuts are there),
        Be boult are smaller for the nut N5 so we kept the Be boult on the left side of the table(where smaller nuts are there),
        Bf boult are bigger for the nut N5 so we kept the Bf boult on the right side of the table(where bigger nuts are there).
        
        so becoz we have nut & boult pair, there are three nuts & boults which are smaller then the current pair that we found. there are two nuts & boults which are bigger then the current pair that we found. img 9.
    
        In img 10. there are two circle, what is that ? 
            These are 'subproblems for us to solve'. 
            ex:-
                initially we had 6 nuts & boults with us, now it's become 3 small nuts, 2 big nuts.
            
            Remember:-
                1.  we have not found the exact match yet. we have just divide it into part.1
                        means we have to still check (in small case)  which boult to nuts.                                                              
                        & also we have to check (in bigger case)  which boult to nuts.                                                              
                2.  Ba match with N5, it was the random selection, so we can't be sure that it will always be 3:2 ration. 
                        means now we have 3 small nuts & boult & 2 bigger nuts & boult but we not sure that always this will be the ratio. 
                        it may be 4:1, where 4 small nuts & boult & 1 bigger nuts & boult, it may be 2:3, where 2 small nuts & boult & 3 bigger nuts & boult.             
                        it may be 5:0, where all 5 small nuts & boult & 0 bigger nuts & boult therefor it is random.    
                        
                this above thing we did that is called Partitioning. (like we didvided into subproblems)
                the element we are selected for the partitioning, this element is actually known as Piviot.   
                
                Piviot is the item becoz of which we divide the data into two sets. so that we can solve the two side seprately. so it is kind of Divide & Conquer Technique. 
                    we are dividing it using piviot element & the process of dividing is known as Partitioning.           
                
                Partitioning is basically, we have set of data. based on the piviot we divide the compelte data into two part, one data is smaller side, another data is larger side.                                            

```
### Given an integer array, rearrange the elements in it. such that for all i if A[i] is less than x(part of input) then it is on left side else on right side of array. A[i] >= x, SC=O(1)         {x is the piviot}
``` 
    A=[9 8 1 6 5 8]         x=6
    
        now, we have to rearrange the elements such that small element are on left side, larger elements are on right side. 
            it can be in any order, like:-
                                small elements are on left side & large elements on the right side.
                            smaller side elements are in any order. bigger elements are in any order. 

            this task is extermely easy if we have extra space. like we just iterate & put it in the array, so we have to solve in costant space. means we have to rearrange the array, like shifting, swapping inside the array only. img 11.

            Sol1:-
                    if we sort the data, small data will be on left side, larger data will be on right side. no matter what the piviot is. 
                        best sorting algo we learned till now is Merge Sort. 
                        TC = O(N log (N)).
                        
            Sol2:-      (Two Pointer approach)                      // do we really need to sort ?
                    if we arrange small data on left side then large data will automatically arranged on right side. vice versa. so do one of the task.
                        ex:- 
                               0 1 2 3 4 5   
                            A=[9 8 1 6 5 8]         x=6                         // small element on left side.
                                
                               we keep i pointer at index 0, it indicating that this is position where we can place small element. 
                               & we iterate the array element with the j pointer. img 12.
                               
                               first element is 9, Is 9<6 = No, so we ignore it & move forward.
                               second element is 8 Is 8<6 = No, so we ignore it & move forward.
                               third element is 1 Is 1<6 = Yes, then element should be placed at the i th index (i=0).so we swap it. after swap then we update the index i=1.
                               fourth element is 6 Is 6<6 = No, so we ignore it & move forward.
                               fifth element is 5 Is 5<6 = Yes, then element should be placed at the i th index (i=1).so we swap it. after swap then we update the index i=2.
                               sixth element is 8 Is 8<6 = No, so we ignore it & stop.
                               if we do this much then, 
                               'all small elements are on left side' & from 'index i till the end large data will be there (right side)'.
                                
                                assume on the left side, there is an small element if we compare with given piviot then if we swap with i pointer then also does not happen anything. img 13.
                            TC = O(N)
                            
                            
```
### Quick Sort  (Divide & Conquer)
``` 
    here, we use only Partitioning.
       0 1 2 3 4 5 6
    A=[7 3 2 5 1 6 4]
        
        Imp:-
                "we select any one element as piviot element".
        
        let say, we take last element as piviot element (random selection).
        now we select 4 as piviot element then 'small element will be on left side & greater than equal to elements will be on right side'.
        there is one extra step over here is "the element 4 takes it's correct place". 
        
        Ques:-  What is the index of the element 4 in the sorted order ?
        Ans :-  index 3, is the correct place for element 4 in the sorted order & all the small element will be on left side & greater than equal to elements will be on right side. img 14. 
            
        the selection of element 4 has divide the array into two part.
        so we have N elements in the array, that divide into two parts (almost half of size). similar to merge sort technique.
        now the element 4 has at correct position, we have to sort the smaller part seprately & lager part seprately.

        Quick Sort Scanerion:-                                      (Best Case Scanerio)
            if N size of array & subproblem has half the size.
            Ques:-  What is the number of levels we will see ? 
            Ans :-  In case of K step becomes equal to 1 = N/2^k, for us to stop (means stopping conditions). that means k= long N. see in pdf.              
            
            Worst Case Scanerio:-  
                In the same input, if we select piviot element as element 7 (randomly) first element.
                In the sorted order the element 7 has to be placed at index 6. so all the small elements to be on left side,  now the subproblem is sort the left side part.  
                so from N size array to reduce the subproblem size is N-1, everytime if its happen (subproblem size reduce to N-1 at every time) then it will take  N-k=1, k=N-1.
                
        Time Complexity:-
                   O(N log(N) <=   Tc of Quick Sort <= O(N^2)
                    Best                                Worst    
           
           While using Quick Sort we should Carefull becoz the worst case (that is Base case for us) TC is O(N^2)
            
        Dry Run:-
            How Quick Sort doing the sorting part:-
                   0 1 2 3 4 5 6
                A=[7 3 2 5 1 6 4]       piviot=4    (last element)
                   
                   3 2 1 4 7 5 6            here, small & large data to sort. 
                   3 2 1                    for small data, again we take the piviot = 1 (last element).                                                     7 5 6     for large data, again we take the piviot = 6 (last element).
                   1 3 2                    1 is the small element so 1 come left, 3,2 element are bigger so they come right. (un-lucky selection)           5 6 7     right place of 6 is middle, 5 will come on left, 7 will come on right.   (lucky selection)
                                            now we have to sort 3 2                                                                                                  for single element 5 & 7 they are already sorted (base case) & they are at right place. (lucky selection)
                     2 3      again we select the piviot=2 (last element), the right place of 2 is mid, now the entire array is sorted. (un-lucky selection)
                
                   Final O/p = 1 2 3 4 5 6. 
                   
                   We are doing partitioning at every step. img 15.
            
        Code:-
            Steps to write the code,
                void quickSort(A, st, end)         we have subproblem of small array so we need to pass the start=0 & end=N-1 index of that array
                {
                    if(st >= end)           means if we don't have array || only one element in the array, 
                    {
                        return                         no need of sorting, just simply return. 
                    }                       if the size of array is greater than 1 then we will do sorting for that we need the partition.
                    
                    pi =  partition(A, st, end);      pi is the index of the partitioned element. so we create the function partition, partition the array A from start to end.     this function return the index of the partitioned element.
                                                      if it is paritioning element 4, then it is giving the index of element 4 after partition. similarly it is giving the index of element 6 after partition. so any element we select, it is giving the index of element that element after partition.
                                                      ex:- the index of element 4 is know, that means from start (index 0) till the index 3 (where element = 4) - 1 which is index 2 we need to partition. & from the index (where element = 4) 3 + 1 till index N-1 that we need to partition. so we apply sorting.
                    quickSort(A, st, pi-1)            pi index is already sorted.
                    quickSort(A, pi+1, end)          
                }   
                    // it is same as merge sort algo, instead of merging step here we have parition step.         
                
                above Quick sort algo is similar to Merge sort. like we have two fun call of smaller size {quickSort()} & another fun call {partition()} which is taking O(N) time. 
                Ques:-  What is diff bw merge step & partition step ? 
                Ans :-  In the merge step SC = O(N) we need extra space, In partition SC = O(1) so the SC of partition is constant so In the quick sort the Space is not ocupied by any temp array.
                
                    Note:-  if we say, SC will always be O(1) in quick sort is not true. becoz "we are using Recursion in Quick Sort" (Recursion Stack will take space for fun call).
                            so SC will be 'No. of levels' which will be between O(logN) in best case & O(N) in Worst case.
            
            TC = 
            SC =    
                
            Steps to write the partition fun code,
               int partition(A, st, end)        we have to partition the array A, from indext start to index end.   
               {                                first task is to select the piviot element.                  
                    pi = A[end];                piviot element is to be select the last element as the piviot element.          it's our choice to make piviot element whatever we want first, last, mid, or any element can be piviot element.
                    i = st;                     keep i pointer to swap the smallest elements, so all the small elements will be on the left side, 
                    for j --> st to end        pointer to travel the array. 
                    {
                        if(A[j] < pi)           means we have to swap it with the index i.          if the element is bigger than pi then we are ignoring it. 
                        {
                            swap(A[i], A[j]);
                            i += 1;
                        }
                    }
                               img 17. we have the array (purple line), all the small elements are placed / swapped on the left side. then the index i will be point to next index (means where the next small element can come).
                                       if all the smaller element || less than pi element are on left side. & the index i will be point to next index but we don't have the small element, 
                                       so, the piviot element which is currently residing at ending index that we can swap with the i.
                    swap(A[i], A[end]);
                    return i;         now after swapping, the index of piviot element is the index i element, so we return i.                   
               }
                               parition fun is basically partioning the array into two parts small on the left side, piviot element is on the right place & large element on the right side.  
               
                    img 17.     previousluy it wans going till N. here we are doing 1 step extra after the for loop, for easy to understand that step we can do insde the for loop also. 
                                Now we are going till end-1, & end index will be piviot element so we will place pi to the current position after the for loop. 
                                
            TC = O(N)
                    
            SC = O(1)  
        
        Dry Run:-       (partition fun)
              
                   0 1 2 3 4 5 6
                A=[7 3 2 5 1 6 4]       piviot=4 
                
                index i which is currently pointing to index 0 & index j to iterate the array. & j will iterate till index 5. index 6 is the piviot index.
                now j=0, Is A[j] < pi ==> No, we will ignore it. we move forward.       Array looks Like:-  7 3 2 5 1 6 4       i=0
                now j=1, Is A[j] < pi ==> Yes, we will swap it with i & increment the i.       Array looks Like:-  3 7 2 5 1 6 4       i=1
                now j=2, Is A[j] < pi ==> Yes, we will swap it with i & increment the i.       Array looks Like:-  3 2 7 5 1 6 4       i=2
                now j=3, Is A[j] < pi ==> No, we will ignore it. we move forward.              Array looks Like:-  3 2 7 5 1 6 4       i=2
                now j=4, Is A[j] < pi ==> Yes, we will swap it with i & increment the i.       Array looks Like:-  3 2 1 5 7 6 4       i=3
                now j=5, Is A[j] < pi ==> No, we will ignore it. we move forward.              Array looks Like:-  3 2 1 5 7 6 4       i=3
                now j for loop is complete.                                                          0 1 2 3 4 5 6
                now we swap index i with piviot element. currently index of i=3 & index of  pi=6. A=[3 2 1 5 7 6 4]   after swapping A=[3 2 1 4 7 6 5]
                return i;       here i=3 A[i]=4.    img 17.
        
        Probablistic analysis of TC:-       (To explain that Quick Sort is actually good)                                               (no need to do us, no one will ask)
        
            Imp:-       (we make sure that subproblems had less than 90%)
            Let say, we have 100 elements in any random order like:- 1 2 3 ....... 9 10 11 ....... 49 50 51 ..........99 100.  
            we are doing the partitioning,
                Ques:-  What is the worst Piviot element, Someone can select ? 
                Ans :-  {1, 100} if we select the piviot element as 1 || if we select the piviot element as 100 then it is not doing anything, it is basically 100 elements will become 99 elements.         
                
                Ques:-  What is the best Piviot element, Someone can select ? 
                Ans :-  {50, 51} if we select the piviot element as 50 then 49 elements are smaller & 51 elements are greater. if we select the piviot element as 51 then 50 elements are smaller & 49 elements are greater. these two elements are center elements, basically when we have even elements then we have two centers. for odd elements we have one ceners. 
                
            if we have N=100 & we have to select the piviot element such that the smaller elements are less than 90% of N (means less than 90 elements) & large side also less than 90% of N.
                means left side data should be less than 90 elements & right side data should be less than 90 elements. 
                
                Ques:-  What are the candidates we have for piviot element ? 
                                                N elements will be divide into subproblems, one subproblem of size is 10% other subproblem of size is 90%. 
                            if we select 20
                                (1 - 19)    (21 - 100)
                                   19           80          elements, so the 20 is the valid piviot.
                            we can select any number but what is the range of that number.  so that left side & right side have 90 elements.
                            
                            if we select 5, how many elements are less than 5. how many elements are bigger than 5. 
                                                4                                 95
                                                so the 5 is not valid piviot. becoz we have make sure that "both the side, no. of elements should be less that 90"
                            
                            if we select 10, how many elements are less than 10. how many elements are bigger than 10. 
                                                9                                 90
                                                so the 10 is not valid piviot. becoz we have make it less than 90, here 90 elements are greater side.
    
                            if we select 90, how many elements are less than 90. how many elements are bigger than 90. 
                                                89                                 10
                                                so the 90 is valid piviot. both the side have less than 90 elements.
                        
                Ans :-  selecting any element from element [11 90] the count of small elements will be less than 90 & the count of large element will be less than 90.
                        Total No. of elements = R-L+1
                                                90-11+1 = 80        means from 1 to 10 elements & from 91 to 100 elements are not considering as good piviot.

            Probability of selecting a piviot that make sure subproblems are less than 90% of original  problem =       total favourable case   /    total case,    80/100  = 0.8   || 80%,
                so 80% chances are there that are subproblems are less than 90% of size.

                Case where we see that subproblems are of less than 90% size,
                    N elements will be divide into subproblems, one subproblem of size is 10% other subproblem of size is 90%. 
                                                                    N/10                            9N/10
                    WE KNOW 80% CHANCES ARE THERE THAT WE CAN DO BETTER THAN THIS above.
                    now N/10 has smaller part                       now 9N/10 has smaller part
                     (10% OF N/10)    (90% OF N/10)                   (10% OF 9N/10)    (90% OF 9N/10)             
                        N/100           9N/100                          9N/100           (9/10)^2 * N
                        .               .                               .                   this is large problem so again 10% 90% will continue.
                        .               .                               .                 (10% OF (9/10)^2 * N)                 (90% OF (9/10)^2 * N) 
                        .               .                               .                  .                                     .
                       these are small sub problem which are end early.                    .                                     .
                                                                                           .     after k step 90% case will be = (9/10)^k * N
                                                                                                 finally we make this (9/10)^k * N = 1.     this implies N=(10/9)^k  which implies K=log BASE OF (10/9) OF n  (it is log but not BASE 2).       these are the no. of levels.
                                                                                                 
                     Understand this  K=log BASE OF (10/9) OF n,
                        usually in the programming question, the size of N we get is 10^5 (size of the array, no. of elements of the array).    
                        then the value of log BASE OF (10/9) OF (10^5) = 109   (it is order of 100 like 10^2).
                        
                        if this {K=log BASE OF (10/9) OF n} is no. of levels, according to quick sort algo the TC is:-
                            n * no. of levels
                            N * (log BASE OF (10/9) OF n)      
                        we found the value of N=10^5, 
                            10^5 * 10^2  = 10^7   
                            
                        Ques:-   Can we have 10^7 iteration in one second in our system ? 
                        Ans :-   Yes, TC = O(N * (log BASE OF (10/9) OF n)) will works for N=10^5.  so 80% of the times we are doing better than this{O(N * (log BASE OF (10/9) OF n))} TC.   
                                    SC will be No. of levels, that is O(N * (log BASE OF (10/9) OF n)). this is also 80% of times we do better than this.         
                     
                     If we use quick sort then it is good becoz it is giving the optimisation is SC.                                   
``` 
### Quick Sort & Merge Sort relationship
``` 
    Merge Sort is best in TC but it takes extra space.
    Quick Sort is good with Space Complexity but TC is probabilistic. 
        like O(n log(N))    ||   O(N^2). it happened that time is O(N^2) so it can give TLE error it it is in Worst case. 
        
    If the size of array is 10^5 Then we should use Quick Sort. becoz TC is worst but SC is optimised here. 
    
    Conclustion:-
                base on the requirments, if we specific with the time then use merge sort, if we want to optimise space & we are ok with time {O(n log(N))    ||   O(N^2)} then we should go for Quick Sort.
```