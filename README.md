## Two Pointer
1.  **We have two variables || position where we have to start & we have to figure out how to use these location to find the ans**
``` 
    Used two pointer approach:-
        -   Merging two sorted array into one unsorted array 
        -   Check if String is Palindrome
```
2.  **Two Pointer is basically is Binary Search Version where we have two variables instead of one**
``` 
        means it will help us to find the parameter with respect to 2 variables.  
```

### Basics:-  Given an sorted integer array A & an integer K. Find any pair i,j such that A[i]+A[j] = K & i!= j. SC = O(1) 
```
    Hint:-  sorted array has given so there is an pattern in that.          **************Imp*******************
             0   1   2  3   4   5   6
        A = [-5  -2  1  8  10  12  15]      k = 11
           Ans = (2,4)
           
            Bruteforce:-
                "for every pair of i,j. check if sum = k"
                    TC = O(N^2)
                    SC = O(1)
                    
                    Code:-  write own (we can do this using two for loop)

            Note:-  
                we have given sorted array & we have to search for something(finding any pair). 
                whenever searching is required in sorted data (which has a pattern) then we can apply Binary Search.      **************Imp*******************
                
                Ques:-  How we can apply Binary Serach ?
                Ans :-  Becoz Binary Search can find only 1 number not 2.   means it help us to find 1 variable.
                
            Binary Search:-
                    Given:- A[i]+A[j] = K
                    let say, we fixed the i, only j is dynamic. means "for every i we have to find the ans" 
                        in that case:- A[j] = k-A[i]  
                        now ques is, "for all i, search if k-A[i] is present in the array"              // like:- i=2, 11-1 = 10, now check is 10 present in the array or not.
                        & for searching we can use Binary Search.
                        
                        TC = O(NlogN)   ==> N is for every i we are traveling & logN is for Binary Search. in pdf.
                        SC = O(1)
                        
                        Code:-  Write own (simple binary search)
                                -   Take care of this case (i!= j) when apply binary search means searching the element then take care about this case.       
            
            Two Pointers:- (TP)  
                         0   1   2  3   4   5   6
                    A = [-5  -2  1  8  10  12  15]      k = 11
                    if the array / input is given to us in the particular pattern, in those case we can apply Binary Search, also Two Pointer approach.
                    Basically Two Pointer is a Binary Search version where we have Two pointers instead of one. so binary search help us to finding one variable, two pointer help us to find the parameter with respect to Two variable.
                    here, we have to find the pair so we can directly apply Two pointer is one of the approach. 
                Problem with TP:-
                    "Where to start with & How to upadate them"     *********Imp Step**************

                    How we can solve ?
                        -   we start from inde i=0 & j=1 becoz i!=j       // no harm in that, this is one way to start that.
                                at this point, A[i] + A[j] ==> A[0] + A[1] = -7. -7 is less than k.             // currently we are at the position where sum < k.
                                to reach the sum = k we will increase the value. now goal is to increase the value of A[i] + A[j]. 
                                    now we have two choices either increase i pointer or j pointer.             // if we increase i or j pointer then the sum will increase becoz array is sorted
                                    
                                   Ques:-   Can we certain that lets increase i or increase j means "is it possible that we can sure that I should increase i or increase j"
                                   Ans :-   we can't be sure 100%, becoz we don't know which one lead into ans. 
                                   
                                   Conclusion till now:-    "there is no certain step to do. there will be OR always" means we have a choice.
                                   
                                   Imp:-   "whenever this choice situation will comes in(we are in choice), where we specifically not descide how to update then consider that we have start in wrong way". 
                                                means if we want to solve the problem using two pointer then this is not the right stat that we do. i
                            
                         Imp1:-   this way we can go for elemination, Baically there will be 2 || 3 possibility to start the pointer & we can descide wethere that particular point is correct or not. 
                                     by just chekcing "can i update it certainly, if not then its not right direction". img 1.
                                     
                                  if we start like i=5, j=6. A[i] = 12, A[6] = 15. 
                                  Ques:-    Will it be a good start ?
                                  Ans :-    No, becoz again the same situation come. sum will more than K. so we have to decrease the value now either decrease i or decrease j. again we can't certain what step we have to do.
                                            img 2.
                                  
                            How to descide that we are not starting correctly. 
                                  mostly these 3 possibility we have to start the pointer and we can descide weather that particular point is correct or not by checking.
                                  like:-
                                        Ques:-  Can I update it certainly 
                                        Ans :-  If not then this is not the right point.
                                  
                                  so we solve any problems using two pointers            (99% problem approach)
                                    -   Start from Begining
                                    -   Start from End
                                    -   Start like i from begining & j from end.
                                        
                                        its all depends on question, from where to start 
                                  
                                    
                            ** "How to descide that we are not starting correctly."
            
                Solution:-      must remember "Array is Sorted".
                        initally, i is at 0, j is at 6. 
                        interesting thing,  A[i] + A[j] compare with k.
                                             -5  +  15    <     11          here, sum is smaller then k. that means we have to increase the sum     10 < 11
                                                                            Ques:-  How to increase the sum ?
                                                                            Ans :-  increasing the sum is possibly by increase i. becoz if we do j-- then ans will get 7 < 11
                        now, we update i:-            i=1 & j=6             whenever we perfrom update || move the pointer then "we certain that i=0 element should not be visited again"
                                                                            becoz if we revisit i=0 then its not two pointer approach. becoz it will not helps to optimise time.
                        Note:-                                              In two pointer approach "we ensure that, when we are living the element that will not be the ans".
                                                                            like:-
                                                                                -5 + largest element in Array will be less than k.
                                                                                    means -5 + any element in the array will also less than k.   
                                                                                so we are updating i. 
                                             -2  +  15      >   13          here, sum > k, so decrease j. 
                                                                            Ques:-  we updating the value of j. can we certainly sure that j=15 will never be the ans ?
                                                                            Ans :-  yes, 
                                                      i=1 & j=5                       becoz, 15 + smallest avalilabe element in the Array will be greater than k.   // Available element means we have remove -5. so consider remaining element
                                                                                             15 + any smallest avalilabe element in A[i] > k. means sum will always increase. so 15 is not the ans.   
                        Till now we got certainity "When should increase i, When should decrease j"    
                                             -2  +  12   <      11          so we have to increase the i.  
                                              1  +  12   >      11          so we have to decrease the j.
                                              1  +  10   =      11          got the ans.
                                              
                Code:-
                        i=0     j=N-1     
                        while(i<j)      // this time, becoz we are removing the elements as we increasing the i, as we decreasing the j. so i should not cross j & not be equal to j. when i=j then only 1 elemnt left in Array.                         
                        {               // three case to check.
                            if(A[i]+A[j] == k)
                            {
                                return i,j
                            }
                            else if(A[i]+A[j] < k)
                            {
                                i+=1
                            }
                            else
                            {
                                j-=1
                            }
                        }
                        return (-1, -1)     // after doing all of these if ans is not present then we return the pair of -1.
                                        // if we find multiple pairs then also we use TP. just do not stop, keep on updating till we found all the pairs.
                                            like:-
                                                    x + y = z   // here, we find multiple pairs like 2+3 = 5 so to find another pair we have to update both 
                                                    2 + 3 = 5   x & y are diff
                                                    1 + 4 = 5   x & y are diff, if we update only 1 var then z should be 1+3 != 5 so update both. means increase i & decrease j both. 
                TC = O(N)               // using Two Pointer we solve this problem in linear time.
                SC = O(1)
                                    // if elements are duplicates then maintain frequecy of every element so that we can find the pairs easily.
```
## **If Any Input has given in Particular Pattern in these case we can apply Binary Search & Two Pointers.**
1.  Input in particular :-  Array is given in sorted way.  (ex)
2.  If the input is unsorted then we can't apply TP. either we want to sort the array first then apply TP or use map, other data structure.
3.  Two pointers only works **When we have certainty**

### Problem 0:-Given an sorted integer array A & an integer K>0. Find any pair i,j such that A[i]-A[j] = K. SC = O(1) 
``` 
             0   1   2  3   4   5   6
        A = [-5  -2  1  8  10  12  15]      k = 11
           Ans = (2,4)
        
        Brutefore Approach:-
            write own code TC (same with above question).
        
        Binary Search:-
            "for all A[j], search for A[j]=k+A[i]". 
            TC (same with above question).
        
        Don't assume above Two Pointer code / approach will work here also, see below what if we start i=0, j=N-1.
        Two Pointer:-
            A[j] - A[i] = 15 - (-5) = 20 > k.  
           
            Ques:-  Decreasing the diff, Can be done by Decreasing the value of k. 
            Ans :-  if we increase the value of i that will also decrease the difference.
                    A[j] - A[i] = 15 - (-2) = 18 > k.           // 20 to 18 the diff has decreased. 
                    
                    so either we increase or we decrease, In both the case Diff can decrease.
                    means we are not certain to that we should update i or j, still we have choice. that means this is not the right way to apply two pointers.
            
            Ques:-  From Middle part we can't do, becoz we can't descide what is middle in case of even elements or odd elements ?
            Ans :-  Middle part is tricky.
                    like:-  
                            A = [-5  -2  1  8  10  12  15]
                            here, 7 elements are there so how to descide weather start from index(2,3) or index(3,4).
                            In odd elements if we need to select two pointers then we don't have the certainity.
                                In even elements if we need to select one pointers then we don't have the certainity.
            That's how we can descide wether we are in right direction or wrong direction.        
        
           Hint:-   inderictly given in the question.
                    k>0, it basically tells us that "A[j] is greater than A[i]" means after doing k-A[i] the sum will be positive, also the array is sorted that means j is greater then i.
                    so if we want to start both the pointer from begining or both the pointer from the end. both of the ways are correct.
                       in both ways we can descide certainly.
                       
                    (K>0 means i!=j) In Home Work question, 
           
           Both the pointers in the End.
            i=5 j=6, A[j]-A[i] = 15-12 = 3
                now we make sure that diff should be increase. now both the pointers are at the ending position. so j we can't decrease so only option is to decrease i.
                 Ques:- If we decrease the i the Does the over all diff decrease ?
                 Ans :-  Yes.
                now we update the i pointer from index 5 to index 4. at this point of time we don't visit again at index 5 for the pointer i.
                    it does not mean that we never visit for index j.
                
                Imp:-
                    A[i] will never have any j, such that A[j] - A[i] = k.              ************Imp*************
                    currently i=5,         
                    there is no j such that the above condition is satisfied.  
                    means we can say that 'we will never have this 12 as A[i] for which any A[j] will give the ans k'. 
                        becoz 'largest element - A[i] is less than k.   
                            eg:- A[j] - A[i] = k, 15 - 12 = 3 which is < k.     
                        so if have any other element - A[i] it will always less than k (it will never get greater value).
                                any element of j we select, if we subtract A[i] like:- 10 - 12 = -2 is < k and so on. it will always less than k.
                    so we are updating i becoz this is satisfied for index 5. so we don't want to visit index 5 as A[i]. img 3.                                           
        
           Both the pointers in the Begining.
              i=0 j=1, A[j]-A[i] = -2 - (-5) = 3, 3<k so we want to increase the value, to increase the value we will increase the j. means update the j pointer. 
              "there will never be any other i for which this particular A[j] = -2 will be satisfied". like A[i]=10 A[j]=-2, -2 - 10 = 12. 
              becoz this element (A[j]=-2) - any other element will always be smaller element.
              
              i=0 j=1, A[j]-A[i] = -2 - (-5) = 3, 3<k       now     j++
              i=0 j=2, A[j]-A[i] = 1 - (-5) = 6,  6<k       now     j++
              i=0 j=3, A[j]-A[i] = 8 - (-5) = 13, 13>k      now     i++
              i=1 j=3, A[j]-A[i] = 8 - (-2) = 10, 10<k      now     j++
              i=1 j=4, A[j]-A[i] = 10 -(-2) = 12, 12>k      now     i++
              i=2 j=4, A[j]-A[i] = 10 - 1   = 9,  9<k       now     j++
              i=2 j=5, A[j]-A[i] = 12 - 1   = 11, 11=k      now     done.
              
              that's how we update the pointers.
              
           Code:-
                 i=0     j=1   
                                Ques:-  What is the stopping conditions ?
                                Ans :-  i<j we can not write becoz i is always less than j(read hint).
                                        when j value reaches the end just stop it, i & j values are increasing always, so there will be a point of time where j reach the end.
                                        i can't reach first becoz i<j.
                                        so (j<n)
                 while(j<N)                              
                        {               /
                            if(A[j]-A[i] == k)
                            {
                                return i,j
                            }
                            else if(A[j]-A[i] < k)
                            {
                                j+=1
                            }
                            else
                            {
                                i+=1
                            }
                        }
                        return (-1, -1)
        
           TC = O(N)    Best thing of TP is the SC is O(1) & Binary Search also.             
           SC = O(1)
```
### Hw Problem.

## Tips:- How to solve any (DS)question with Duplicate elements.
``` 
    let say, we know the solution of any problem (of any data structure) with unique elements then it is always possible to solve the exact same problem in case of duplicates.
    To make this(duplicate element) simple, we simply use 'Frequecy Array for duplicates parts || Frequency Map in case of Ranges'. 
    like:-
        If we know how to solve any problem where this below input in present,
        [2 3 10 15]
        
        there is an example, where this below input in present,
        [2 3 3 10 10 10 15]
        
            then we can do is,
            [2 3 3 10 10 10 15]
                update this like,
             2 3 10 15  and for every elements store how many times that element is present. 
             1 2  3  1  that many times elements are present.
        
        assume we have to find the pair with sum z.
        if there are 3x & 2y then total 6pairs will be there with sum z.
        so the 'frequency can tell you how many counts will be there'.
    
    so, no need to solve duplicates seprately or doing complicated stuff just use frequecy array & that's it.
                
```
**Two Pointer Basics done**
#### This below is also implortat place where Two Pointer used.
### Problem 1:-  Given an Integer array of +ve elements (unsorted). we have to Check if there exist a subarray with sum=k.
``` 
      0 1  2  3  4 5  6
    A[1 3 15 10 20 3 23]        K=33    Ans=True.
                                K=43    Ans=False.
                                
        Ques:-  Subarray of array Size N ?
        Ans :-  N*(N+1)/2
        
        Bruteforce:-    
                "Check every subarray sub sum", TC= O(N^2), SC= O(1) While calculating subarray, at runtime we get the sum. means while looping through the subarray we also get the sum.
        
        Hint:-
                "Whenever any subarray ques is given for which we have to find the sum" then the easy way to calculate the subarray sum is:-   Using Prefix Sum.
                
                    A[1 3 15 10 20 3  23]   k=33
                    P[1 4 19 29 49 52 75]   P[i] = P[i-1]+A[i];   
                                            TC = O(N), SC = O(N) || O(1) If we modify input array.
                                            
                    If we have to find out the subarray sum from index i to j. What does it look like using the prefix sum?                       
                 Ques:- If we have to find out the subarray sum for 10 20 3. What does it look like using the prefix sum?   
                 Ans :- Subarray sum(i to j)  ==>  P[j] - P[i-1]
                        52-19 = 33.    img 4.      
                        
                        Ques:-  Is It always this case P[j] - P[i-1] ?
                        Ans :-  only if our i is greater then 0 then this will be the case. 
                        
                        if(i>0)
                        {
                            P[j] - P[i-1];
                        }     
                        
                        if(i==0)
                        {
                            P[j];
                        }  
                 Now what we have to do is, 
                    we have to do is "check if P[j] Becomes k at any point" &  we have to "check if P[j] - P[i-1] Becomes k at any point". means Subarray Sum = k. img 5. 
                    check if any P[j] = K || any P[j] - P[i-1] = k.     
                    
                    Ques:-  Checking in the array, if any value (P[j] = K) is equal to k ?
                    Ans :-  easy, While calculating prefix sum array we can also check this (P[j] = K).
                            like:-  Is there any value that equal to k, if yes then return that.
                    
                    Ques:-  Do we know how to find pair with given difference = k ?
                    Ans :-  O(N). (In previous sum) but there was a condition in the previous question that we have 'sorted array'.
                            but here we have unsorted array so,
                             
                             Ques:- how will be the TC = O(N) || how we can apply the TP approach. 
                             Ans :- here input array is not sorted, we are not applying two pointers on input array. we are applying two pointer on Prefix array & prefix array is automatically sorted.
                                    In that prefix array we have to find the pair with difference. it is like previous question that we did.             **********Imp***************
                             so, Total 
                                    TC = O(N)
                                    SC = O(N) || O(1) if we update the input array.
                
                This part(P[j] - P[i-1]) we can solve using previous problem 
        
        we are not finding Each sub array sum in this question. we are trying to findout sum of subarray which is equal to k.
        
        In Interview, he asked that 'solve this problem using SC=O(1) but without updating array'.
            we can solve it using prefix array technique, using "Carry Forward Technique", it is nothing but 'Prefix Array idea without Prefix Array'.
            
            A[1 3 15 10 20 3  23]   k=33                i to j ==> indicating the sub array.
                initially we can travel from either Left to Right or Right to Left, both are correct.
                initially there is 1 element in the subarray, now this particular 1 element in the subarray has sum less than k.  img 6.
                    so we try to include the next element, therefore sum will increase. again sum is less than k so we try to include the next element, therefore sum will increase.
                    again sum is less than k so we try to include the next element, therefore sum will increase. now sum has greater then k. img 7.
                    
                    conclusion:- 
                        C1:-    "Till sum is less than k, we are increasing j" || sum < k     ==> j++. means adding more & more element to sum becomes k.
                        C2:-    "If sum is larger than k, then we have to decrease the elements". means increasing the i. ||  sum > k       ==> i++. means deleting the elements from the sub array.
                        
                    now sum has greater then k, so we decrease the i (C2).
                    for index 0 || A[0], both index i & index j are updated. (like:-     i=1, j=4.   img 8.) 
                    that means A[0] can never be in the Ans (becoz both i & j are updated).
                        Ques:-  Why this A[0] Cannot be in the subarray with sum=k ?            **************Imp***************
                        Ans :-  for this element (A[0]) to be the starting point, we already check these elements (brown color line), if any of these elements (brown color line) has selected as the end point for A[0]
                                    then the sum<k.     means when i at index 0 & j was index 1 2 3. the sum was less than k.
                                    when this element (20) was j, at this particular point sum > k. so even if we include the more elements means increasing j. like 3 23 then also sum will greater than k. img 10.
                                so, all of the ending points where sum < k. (3 15 10) & we have the ending point where sum < k & we add more elements then sum will always increase, so sum will never be equal to k.
                                therefore we can say A[0] will never be in the subarray sum = k. 
                see the dry run, img 11. 
                the subarray sum = k, the subarray is i to j (3 to 4).  
            This is also TP approach when the subarray sum is finding. 
            
            subarray is from i to j. so i is always <= j. basically if i==j that means we are looking for one element.
            usual Code:-
                i=0, j=0        sum = 0;
                while(j<N)            // here also, j is first reaching to the N. 
                {
                    if(sum == k)
                    {
                        return true;
                    }
                    else if(sum < k)
                    {
                        sum += A[j];
                        j++;    // means add more value to sub array.
                    }
                    else
                    {
                        sum -= A[i];
                        i++;  // decrease the value of sum.
                    }
                } 
                return false;   // if ans is not present.
                
            TC = O(N)
            SC = O(1)
            Ques:-  Will this code work || Is this the right way to write code within TP, like updating i j ?
            Ans :-  No, here we are not checking when the subarray ends at the last index.
                    
                    Dry run 1:-
                                      0 1 2 3
                            like:-  A[5 2 4]        K=6  
                            
                            sum --> 0 => (0+5) 5 => (5+2) 7 => (7-5) 2 => (2+4) 6
                            
                            i   --> 0 -->                         0    => 1
                            j   --> 0 -->   0    =>    1    =>    2 -->      2 => 3     as soon as j=3, the while loop will stop & it return false. but it should be true.
                            
                         updated Code:-
                                i=0, j=0        sum = 0;
                                while(j<N)            // here also, j is first reaching to the N. 
                                {          
                                    if(sum < k)
                                    {
                                        sum += A[j];
                                        j++;    // means add more value to sub array.
                                    }
                                    else
                                    {
                                        sum -= A[i];
                                        i++;  // decrease the value of sum.
                                    }
                                    
                                    if(sum == k)
                                    {
                                        return true;            *********Imp******  -->     Checking the sum after the updates are made is returning true.      so the statements are in correct order. img 12.
                                    }
                                } 
                                return false;   // if ans is not present.    
                                
                     this code is not working fine. for below case     rewatch for dry run 01:50:00.
                     
                    Dry run 2:-  
                                      0 1 2 3
                            like:-  A[5 2 4]        K=4
                            
                                i=0
                                j=0
                                sum=0
                                  
                                No. of iteration 
                                        1.      sum<k (0+5) 5 with j=1 i=0.
                                        2.      sum>k (5-5) 0 with j=1 i=1.
                                        3.      sum<k (0+2) 2 with j=2 i=1.
                                        4.      sum<k (2+4) 6 with j=3 i=1. if sum==k so return false.      this is not the correct ans.
                                        
                                What is the issue over here. 
                                    the issue is 'when we added A[j] & reach the j to N, after that may be there is an subarray which will exclude A[i] like 2' so we never tried excluding here. that was the misktake.
                                    
                                One idea that we should follow always is:-      **********Important***********
                                    right now we are doing, 'When we have particular i & j the subarray sum was calculated from i to j-1 (means we were adding j & then increasing j so j was not part of the subarray)
                                        Whenever we solve the subarray problem "Try to have i to j as Subarray".   
                                        Ques:-  What it means is ?
                                        Ans :-     
                                                let say, we want to start with subarray which has empty subaary like sum=0. || we we want to start with subarray which has the first element has A[0] so we have sum=A[0].  
                                                    means "we can start from the first subarray sum=A[0] that is first element already present in the subarray sum".  like sum=5.
                                                            now if the sum is smaller (sum<k like 5<k) then "first we will increase the value of j then we will add the value to sum" but after increasing j we reach the index N then ?
                                                            we should 'breakout' becoz we can't add anymore.
                                                 summary:- from i to j sum is calculated (sum=A[0]), if the sum is smaller increase j & add that value to the sum. if the sum is greater then decrease it. if its equal then return true. 
                                                           sum==k will be at the top otherwise we will not have the first checking condition & sum=A[0] so we have put it at the top, if sum=0 then we put it at the end.  
                                
                    Final Code:-                        
                                i=0, j=0        sum = A[0];
                                while(j<N)            // here also, j is first reaching to the N. 
                                {
                                    if(sum == k)
                                    {
                                        return true;            
                                    }
                                    
                                    if(sum < k)
                                    {
                                        j++;    
                                        if(j == N)
                                        {
                                            break;
                                        }
                                        sum += A[j];
                                    }
                                    else
                                    {
                                        sum -= A[i];
                                        i++;  
                                    }
                                    
                                } 
                                return false;   // if ans is not present. 
                                
                                0 1 2 3
                              A[5 2 4]        K=4
                              
                              i=0, j=0      sum=5
                              
                              No. of iteration.
                                            1.      sum==k --> No it's greater, (5-5) 0 with i=1 j=0.
                                            2.      sum==k --> No it's smaller, j++, (0+2) 2 with i=1 j=1.
                                            3.      sum==k --> No it's smaller, j++, (2+4) 6 with i=1 j=2.
                                            4.      sum==k --> No it's greater, (6-2) 4 with i=2 j=2.       now sum==k so we stop it & return true.  before reaching at the end its returning true. like j is still 2 not 3.
                                            
                         
                     Note:-
                            while writing the code, handle the corner case with the small small example if its working then good otherwise there was something missing. we can handle it using multiple ways,
                    
                    if -ve elements are there then we can't apply this approach. becoz we increase the subarray size, the subarray sum will not always increase.  
                    so the reason why we have +ve elements is to see if the subarray size increases then the sum increases. like Prefix Sorted array.
                    so In negative elements we can't apply TP approach.
```
### Containter with Maximum Water:-  We have an array where every element of the array is height of the wall. Find two walls that can form a Container to hold maximum water (Maximum area).
``` 
    Disclamer:-     This is not same as Rain Water Trapping Problem, it is similart to Rain Water Trapping Problem there is some difference like In Rain Water Trapping we have to find total area, here we have to find maximum area so we can select any two walls.
    
    There are few walls given to us like 2 4 6 8 10. 
    like:-  
            wall-1 has height 4, 
            wall-2 has height 2, 
            wall-3 has height 10,
            wall-4 has height 4,
            wall-5 has height 8,
            wall-6 has height 2,
            wall-7 has height 6,
            wall-8 has height 2,    img 13.
     
    Ques:-  What is the meaning of Maximum Water ?
    Ans :-  In practical world we can calculate amount of water using Volume like in Liters.   here we don't have 3d version only 2d version. so the amount of water we can calculate in terms of area. 
    
    Ques:-  How we can calculate the area ?
    Ans :-  this area is calculating 'for any index i,j we select, the area will be "Height * Width", so Height will be Min[A[i], A[j])'. we are selecting min becoz the Water can Overflow.
            ex:-
                    we try to store water between wall-5 & wall-7.
                    the water can be store till wall-7, if we store more water then its overflow from minimum side. means minimum of two heights.  
    
    Ques:-  What will be the width ?
    Ans :-  Height will be the diff between the two index.  j-i, considering j>i or |j-1| means absolute value of j-i.
    
    Formula:-
            Height          *   Width
            min(A[i], A[j]) *   |j-1|
    
    Goal:-  we have to findout the two walls which can store the maximum area of water.
    
    If we select wall-5, wall-7 then what is the area ?
        Min(8,6) * |7-5|
            6    *   2  =   12      img 14.
        img 15.
        img 16.
        so the diff pairs of walls the area will be different.
    
    Ques:-  What are the two walls we select that can maximise the area ?
    Ans :-  
            if we select wall-3 & wall-7 then,
                min(10,6) * 4
                    6*4 =   24.
                    
            if we select wall-1 & wall-7 then,          (if any wall in between are gone)
                min(4,6) * 6
                    4*6 =   24.
    this is the maximum possible area that we can have 24.      
    
    So, Given a input which has height of each wall, we can select any two walls & we have to find out maximum area that we can have.
    
    Approach:-
                initially i start from 0, j start from N-1.
                if we move i on right side || move j on left side, 'The Width will always decrease {|j-1|}'.
                when the width is decrease then To increase the maximum area we should try to maximise this {min(A[i], A[j])}. means we should update such that this value {min(A[i], A[j])} increases. 
                so we update the j pointer (7 to 6) becoz the height of j pointer has smaller.
                when we are updating it then we should certainly sure that j=2 value will never consider in future.
                but we can't say that j=2 || wall-8 cannot be in the ans, becoz it (j=2) may be one of the walls in the ans. but if this (j=2) was in the ans then it can consider, right now we are not comparing value.  
                    this value(j=2) is consider with respect to i=4
                Ques:-  Can this wall-8 have the area bigger then area=14 ?
                Ans :-  
                        for this particular element j=2 || wall-8, if we pair this particular element j=2 with any other wall then the best height we can have is:- max H = A[7] = 2.   
                            like:-
                                wall-3, wall-8 ==> max H = ?
                                 min(10, 2)    ==> max h = 2
                            max H = 2.
                            even we pair with very small wall then this small wall will be consider has max H.
                Ques:-  What is the maximum possible width we can have ?
                Ans :-  maximum possible width is i=0, j=7.
                            |7-0| = 7
                            max W = 7.
                so the best possible area that this walls could given us, we are taking already that into consideration 2*7 = 14. & then we are updaing the j value to find the better area / ans then 14.
                therefore this wall-8 will not gives us better ans than 14, so we update this particular wall-8 to wall-7 || index 7 to index 6.
                
                this wall-8 j=2 will give us max to max 14 as the ans, not more than 14. so if we want to find the ans better than 14 then we have to update this wall-8.
                
                the reason why this wall-8 give us 14 as the max ans, becoz the height of the container (maximum area) in which one of the wall is this wall-8 will be 2 & the width of the container will be max to max 7
                    so 7*2 = 14.
                
               0 1  2 3 4 5 6 7
            A=[4 2 10 6 8 2 6 2]                    area = min(A[i], A[j]) *   |j-1|
            
                                                    i   |   j   |   area            |   ans
                                                    ----|-------|-------------------|----------------
                                                    0   |   7   |   2*7 = 14        |   14
                                                    0   |   6   |   4*6 = 24        |   24           we found the better ans from 14.  which wall is smaller i,j ==> i is smaller so we update the i. means this i=4 can't give us the ans better than 24 with respect we pair with any. 
                                                    1   |   6   |   2*5 = 10        |   24           area is smaller so we will not update the ans. now smaller wal is i=2 so we update the i. 
                                                    2   |   6   |   6*4 = 24        |   24           it is already in the ans so not change in the ans. now j is smaller. so we update the j.
                                                    2   |   5   |   2*3 = 6         |   24           area is smaller so we will not update the ans. now j is smaller. so we update the j.
                                                    2   |   4   |   8*2 = 16        |   24           area is smaller so we will not update the ans. now j is smaller. so we update the j.
                                                    2   |   3   |   6*1 =  6        |   24           area is smaller so we will not update the ans. now j is smaller. so we update the j.
                                                    
                                                    now i& j are equal means there are no two walls only one wall is there.
                                                    among all of these just keep track of which ever has largest value. that largest value is the ans.
                                                    
                                                    if one wall is of smaller height then increase. if(A[i] < A[j]) will increase i++. other wall smaller height then we increase j-- if(A[j] < A[i]).
                                                    when both the walls are equal then we update both i,j. assume A[i]=2 A[j]=2 for both the walls we have calculate best Area so we upadate both of them.  img 17.
    
    Code:-
            write own.
            just calculate the area whichever is smaller update that height & store the ans.
    
```