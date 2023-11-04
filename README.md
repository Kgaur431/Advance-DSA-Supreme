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

### Problem1:-  Given an sorted integer array A & an integer K. Find any pair i,j such that A[i]+A[j] = K & i!= j. SC = O(1) 
```
    Hint:-  sorted array has given so there is an pattern in that.
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
                    let say, we fixed the i. means "for every i we have to find the ans" 
                        in that case:- A[j] = k-A[i]
                        now ques is, "for all i, search if k-A[i] is present in the array"              // like:- i=2, 11-1 = 10, now check is 10 present in the array or not.
                        & for searching we can use Binary Search.
                        
                        TC = O(NlogN)   ==> N is for every i we are traveling & logN is for Binary Search.
                        SC = O(1)
                        
                        Code:-  Write own (simple binary search)
                                -   Take care of this case (i!= j) when apply binary search means searching the element.   
            
            Two Pointers:- (TP)  
                         0   1   2  3   4   5   6
                    A = [-5  -2  1  8  10  12  15]      k = 11

                    here, we have to find the pair so we can directly apply Two pointer is one of the approach. 
                Problem with TP:-
                    "Where to start with & How to upadate them"     *********Imp Step**************

                    How we can solve ?
                        -   we start from inde i=0 & j=1 becoz i!=j       // no harm in that, this is one way to start that.
                                at this point, A[i] + A[j] ==> A[0] + A[1] = -7. -7 is less than k.             // currently we are at the position where sum < k.
                                to reach the sum = k we will increase the value. now goal is to increase the value of A[i] + A[j]. 
                                    now we have two choices either increase i pointer or j pointer.             // if we increase i or j pointer then the sum will increase becoz array is sorted
                                    
                                   Ques:-   Can we certain that lets increase i or increase j means "is it possible that we can sure that i should increase i or increase j"
                                   Ans :-   we can't be sure 100%, becoz we don't know which one lead into ans. 
                                   
                                   Conclusion till now:-    "there is no certain step to do. there will be OR always" means we have a choice.
                                   
                                   Imp:-   "whenever this choice situation will comes in(we are in choice), where we specifically not descide how to update then consider that we have start in wrong way". 
                                                means if we want to solve the problem using two pointer then this is not the right stat that we do. i
                            
                         Imp1:-   this way we can go for elemination, Baically there will be 2 || 3 possibility to start the pointer & we can descide wethere that particular point is correct or not. 
                                     by just chekcing "can i update it certainly, if not then its not right direction". 
                                    
                                  mostly these 3 possibility we have if we solve any problems using two pointers.           (99% problem approach)
                                    -   Start from Begining
                                    -   Start from End
                                    -   Start like i from begining & j from end.
                                  
                                    
                            ** "How to descide that we are not starting correctly."
            
                Solution:-
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
                                                                                so we are updating i. 
                                             -2  +  15      >   13          here, sum > k, so decrease j. 
                                                                            Ques:-  we updating the value of j. can we certainly sure that j=15 will never be the ans ?
                                                                            Ans :-  yes, 
                                                      i=1 & j=5                       becoz, 15 + smallest avalilabe element in the Array will be greater than k.
                                                                                             15 + smallest avalilabe element in A[i] > k.       // Available element means we have remove -5. so consider remaining element
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
                        return (-1, -1)
                                        // if we find multiple pairs then do not stop keep on updating till we found all the pairs.
                TC = O(N)               // using Two Pointer we solve this problem in linear time.
                SC = O(1)
                
```
## **If Any Input has given in Particular Pattern in these case we can apply Binary Search & Two Pointers.**
1.  Input in particular :-  Array is given in sorted way.  (ex)