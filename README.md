## Sorting
1.  Sorting is basically arraining an element in the particular order.
``` 
    Ques:-  What is the TC to Find the maximum element in a Random Integer array ?
    Ans :-  O(N).
            We will simply iterate & keep track on every element & store the maximum element in the variable.
            like:-
                A[5 8 1 15 7 6 2]
                img 1.
            
            TC = O(N)
            SC = O(1)
                
    Ques:-  What is the TC to Find the second maximum element in a Random Integer array ?
    Ans :-  There are two approach.
            1.  we have first iterate the array to find the max element.
                then iterate to find the second max element.
            
            2.  one simple for loop, we can track a max element & second max element.
            
            TC =  O(2N) = O(N)
            SC = O(1)
    
    Ques:-  What is the TC to Find the Third maximum element in a Random Integer array ?
    Ans :-  same approach.
    
    If we apply the same approach & we keep on increasing like first max, second max and so on, at certain point we can find k th maximum element.
            TC = O(KN)
            SC = O(K1)  // we might use k seprate variable.
                  0 1 2  3 4 5 6
                A[5 8 1 15 7 6 2]   k=4
                
                    first largest element is:-  15
                    second largest element is:- 8
                    thrid largest element is:-  7
                    fourth largest element is:- 6       we have to find 6.
                    
                    we can apply the above approach to keep track on first, second largest and so on.
                    
                    But can we not use extra variable {O(1)} & still track first largest, second largest and so on.
                
                    
                    Approach:-
                        if we iterate first & we find the largest element. we will have the element 15. 'we want to store largest max but we don't store in variable' so we store in the array, "we just swap the largest element with the last element || first element" 
                        now largest elememnt will be at the last.  it is same as storing in variable. img 2.
                            k=1,     img 2.         // assume, we finding the first largest element. 
                        
                        now we are doing for k=2 means again we have to find the largest element but we are only look at the first 6 element (we will ignore the last element).
                        among the 6th element the largest element we get is 8, now we swap the element 8 with second last element.
                            k=2     img 3.
                            
                        now we are doing for k=3 means again we have to find the largest element but we are only look at the first 5 element (we will ignore the last 2 element).
                        among the 5th element the largest element we get is 7, it is already at the correct position so we don't need to swap the element 7 with any other element.
                            k=3     img 5.
                        
                        now we are doing for k=4 means again we have to find the largest element but we are only look at the first 4 element (we will ignore the last 3 element).
                        among the 4th element the largest element we get is 6, now we swap the element 6 with second fourth element 2.
                            k=4     img 4.
                        
                        Final array look likes:-
                            k=4 [5 2 1 6 8 15]
                        
                        The fourth largest element is 6.
                        
                        Ques:-  What if we apply same approach to find k = N-1 then what will be the final output ?
                        Ans :-  if we continuing doing this then "It will become a SORTED Array".
                                
                                output:-    K=N-1   || k=6
                                            [1 2 5 6 7 8 15]
                        
                        This entire approach is one of the sorting algorithm called Selection Sort.
                        
                        Selection Sort:-    (Basic sorting algo)   
                                    "it says pick up the largest element & placed it in the last position, pick up the second largest element & placed it in the second last position and so on". it is in ascending order,
                                    if we want in Descending order then "pick up the largest element & placed it in the first position, pick up the second largest element & placed it in the second position and so on". it is in descending order".
                                                                            ||
                                    if we want in Descending order then "pick up the smallest element & placed it in the last position, pick up the second smallest element & placed it in the second last position and so on". it is in descending order".
                        
                        TC = O(N^2)
                        SC = O(1)
                        
                        Code:-      this is one of the ways to write it.
                              
                              for i --> N-1 to 1        // it defines the ending position, so right now we are looking for N-1 element then N-2, N-3 and so on.
                                maxId = 0               //  index of maximum element which we are finding.              { here we are assuming that 0 th index is the largest element.}
                                for j --> 1 to i        //  index 1 to i, we are finding whichever the largest element  { then among 1 to i whichever is the largest element we are picking up} 
                                    if(A[j] > A[maxId])
                                    {
                                        maxId = j;      // basically we are storing the index of the largest element in the array from starting till index i.
                                    }
                                swap(A[i], A[maxId]);   // after doing all of this we have the sorted array.
                                
                        Dry Run:-
                            Step1:- find the largest element swap with the last position. 
                                for i --> N-1 to 1
                                    we are starting from N-1 to 0 so we are trying to place the element at the last position then second last position and so on.
                                
                            Step2:- continue till N-1 step  (means find the largest element among 5 elements, among 4 elements ... till N-1)
                                maxId = 0               
                                for j --> 1 to i
                                   from 0 to i, whichever is the largest element we are finding that largest element  
                                
                            Step2:- and swap with last position, second last position and so on.
                                swap(A[i], A[maxId])   
                                   and we are swapping with the i th position.
                                   
                                   
                        Diff b/w Selection || Bubble sort ?
                            In Bubble sort there is an restriction that we are able to swap only adjacent element, but in Selection Sort we pickup the element placed it in right position and so on.   TC of bubble sort & selection sort is exactly same.
                            so, if we have to find k th largest element then we can use selection sort approach. it will take O(K*N) TC, & if k is high then eventually selection sort makes the array as sorted.   
                            
                        certain postion & searching for the elements        ==>     use selection sort.
```
## it's not like we have to write our own sorting algorithm in most of the case we use inbuilt function. **we should know what are the sorting algorithm which are there, which can be used if required, if inbuilt fun are not allowed**
### Problem 1:- Given an integer array where **all odd elements are sorted** & **all even elements are sorted**
``` 
    A=[3 9 2 4 15 10 19]
    
    o/p=[2 3 4 9 10 15 19]
        
        becoz all elements are sorted & all even elements are sorted, so we can seprate out odd elements & even elements.
        once all odd & even elements are seprate out then we can fill in the array.
        [3 9 15 19]      [2 4 10]
        
        now, if we have to find out smallest element of the array. it will be smaller of these two element (odd or even element) 2,3. means it will be either the min odd element or min even element. img 6.
        so, simply make a i pointer over 3 & make a j pointer over 2 & whichever is smaller take that up. img 7. 
        then update j. 
        then which ever is smaller 3,4 so 3 is smaller then update i. and so on. at the end all the even elements are done so whatever is remaining in the odd part just take it as it is in the array becoz odd part is already sorted.
        at the end we get the sorted version.
        we are selecting the array by smallest of the two elements
        
        
        Ques:-  How much it will take to odd & even seprately ?
        Ans :-  O(N)
        
        Ques:-  What is the time complecity to merge back to the array ?
        Ans :-  O(N)
        
        so,
         TC = O(N) + O(N) = O(N)
         SC = O(N).
         
        Common Confusion in Interview,
        Ques:-  Can we do it in Constant space ?
        Ans :-   
                Like:-
                       0 1 2  3 4 ....
                    A=[1 3 7 13 2 ....]
                        
                        odd smallest element are 1 (0) & even smallest element are 2 (4) . & now smaller of these two is 1. 1 is at correct position. img 7.
                        now we increment the i (1). at the index 1 we want to place element 2 becoz even element is smaller.  
                            so if we swap element 2,3 then we can say that odd elements are no longer (img 10, here odd element order is 7 13 3)  sorted. img 8. 
                            & if we want to maintain the sorted order  of odd elements then we can remove element 2 from index 4 & shift every element on the right side. img 9 but it will take more time to shift the element for one swap.
                            therefore shifting the elements will increase the TC. means it will be linear Time Complexity for every one element so overall TC is O(N^2)
                        So we need the extra Space to do this task in O(N), in the same array we can't do this task.  
                        
                        the Merging part that we are doing using two pointers i & j. 
                            Ques:-  Is should necessary that 1 part has all the odd elements & 2 part has all the even elements. || we can do any two sorted array's combine into one sorted array. 
                                                                                ||
                            Ques:-  Merge Two sorted array into one. Can we use Two Pointer Approach ? (it is base of merge sort algo)                     ****************Imp**********************
                            Ans :-  There are some cases that need to handle.
                                    ex:-
                                        we have to find the Ans A which is having N+M elements. Like:-  A[N+M]              // we have to combined the result in A.
                                        B is the first input with N element. Like:- B[N]
                                        C is the first input with M element. Like:- C[M]
                                        both of them are sorted. 
                                        no. of elements are different. N, M.
                                        
                                        Easy Way to do this task:-
                                            1.  just create two pointers.   one pointer (i) used to travel the Array B.  another pointer (j) used to travel the Array C.
                                            2.  we will iterate & fill the enteries in the A one by one.
                                            3.  k loop will start from 0 to N+M-1, becoz total no. of elements are N+M.
                                                Ques:-  Can we directly Compare i element j element & descide which one is smaller ?    || Is there any condition which may go wrong while doing this ?
                                                Ans :-  
                                                        1.  What if one of the array is completely full / done, what happened in that case.        if both are equal then we can take element from any side.
                                                                like:-  
                                                                    if(i == N)      it means the B array has completely travelled. so take the elements from the C array,
                                                                                    A[k] become C[j] & then increment the j+=1;
                                                                        
                                                                       extra:-
                                                                        i==N   here, we are comparing with N not N-1. if we compare with N-1 that means there is last element to compare becoz i start from 0. 
                                                                                i==N means we completed the array B. 
                                                                                    ex:-
                                                                                        N=2     M=5
                                                                                        if(i==N-1)  B array has only 2 elements & i start from 0, so 0 & 1 these two elements are present in the array B so if we compare with N-1
                                                                                        then we are actually compare with element 1 that is present in the array B. & we are handling the case where we travelled complete array B.
                                                                                        so N is the position which indicates that array B has travelled becoz i start from 0.
                                                                    
                                                                    if(j==M)        it means the C array has completely done. so take the elements from the B array,
                                                                                    A[k] become B[i] & then increment the i+=1;
                                                        
                                                        2.  Is it possible that both the arrays are completely full. 
                                                                total no. of elements in B is N.
                                                                total no. of elements in C is M.
                                                                we are travelling N+M times, if B is complete, if C is complete it means the for loop is complete.  so it will never happen that both are complete.
                                                                    either the array B has done or the array C has done.
                                                        
                                                        3.  If none of the array has done, then which ever is smaller we can take & we can also take are of equality.
                                                                else if(B[i] <= C[j])
                                                                        {
                                                                            A[k] = B[i]
                                                                            i+=1
                                                                        }
                                                                else                // reverse of above
                                                                        {
                                                                          A[k] = C[j]
                                                                          j+=1
                                                                        }
                                                        
                                                        Basically these 4 condition we have to handle.  img 11.
                                                        
                                                        see, 
                                                            if(j==M)   else if(B[i] <= C[j}        these two condition are doing exactly same. so we combied them into one.    img 12.
                                                            
                                                            In img 12. What mistake ususally do is, if we combine these two{if(j==M)   else if(B[i] <= C[j}} then we combine these two {if(i == N) else} also becoz these are also doing same thing.
                                                            if we combine these two {if(i == N) else} then we have to take care of one case which is that 'i != N' means there are element remaining in the B array we have to check are there elements remaining in the C array.
                                                                then only we can combine this.      means if one of the array is not done, we have to check wether the second array is full or not.     becoz these two condition {if(i == N)  if(j==M)} first we have to check.
                                                                if we do not check these condition then we get an error ArrayIndexOutOfBound. so these are two condition which first we have to check,
                                                                    Is there any array which is full then do copy otherwise simply compare the elements.
                                                        
                                                        Final Code:-    Img 13.
                                                        Dry Run:-
                                                                    initally, Img 14.
                                                                    iteration 0:-
                                                                       these two condition {if(i == N)  if(j==M)} are not satisfied, so  {(B[i] <= C[j]} so A=[0] & i++ (1).
                                                                    iteration 1:-
                                                                       these two condition {if(i == N)  if(j==M)} are not satisfied, so  {(B[i] <= C[j]} so A=[0 2] & i++(2).
                                                                    iteration 2:-
                                                                       these two condition {if(i == N)  if(j==M)} are not satisfied, so  {(C[j] >= B[i]) means else part } so A=[0 2 4] & j++.
                                                                    iteration 3:-
                                                                       these two condition {if(i == N)  if(j==M)} are not satisfied, so  {(B[i] <= C[j]} so A=[0 2 4 5] & i++ (3).  Now, i is equal to N.
                                                                    iteration 4:-
                                                                       now the condition {if(i == N)} are satisfied, so this condition (i == N) will keep on coming true & we keep on taking element from array C & increment j. 
                                                                       A=[0 2 4 5 6 10] Done.
                                                                       
                                                                       {if(i == N)} are satisfied then copy from right side. 
                                                                       {if(j == M)} are satisfied then copy from left side. 
                                                                       so we have to make sure that these two condition are check.
                                                                    see in pdf.
                                                                       
                                                                    Summary:-   
                                                                            'if any of the array is completely travelled then take the elements from the another array'
                                                        TC = O(N)                 
        
```
## Merge Sort Algorithm (Divide & Conquer algorithym)
``` 
    Divide & Conquer:-
                it is actually very old way of conquering. 
                   if we have big task to do then divide into small small task then do the small part seprately. instead of solving complete thing, divide & solve           ==> basic idea of Divide & Conquer.
                
                   0 1 2 3 4 5 6 7 8 9
                A=[9 8 7 3 6 4 1 5 0 10]
               
                Ques:-  What Merge sort says ?
                Ans :-  Instead of sorting complete array, lets divide into part & then sort the two part seprately.
                
                Ques:-  If we have to choice between two things ?
                Ans :-  that is, divided like img 15 may be (case1) || divide like img 16 (case2).
                        case2 is selected.
                        Reason is:-
                            if we select case1, although the one element 10 is not the problem, but we still have not reduce the size of sub problem, it's almost look like the main problem img 17.
                            
                            but if we divide into half then the size of subproblem become half.
                            & the advantage of dividing the problem into half is 'directly impact on TC'
                            
                Idea of Divide & Conquer:-
                    "Whenever we have big problem we have to divide it, so that evey sub problem is significantly small", it should not be like we are seprating 1 part like element 10, it should become two seprate very small problem 
                    to solve.           
                    
                    Divide & Conquer are recursion based approach.   
                
                Steps on Merge Sort:-   
                    1.  Divide the array A into two parts. img 18.
                        1.1 First part will contain 9 8 7 3 6
                        1.2 Second part will contain 4 1 5 0 10
                        
                        If we 5 elements then we can divide intl 2:3 || 3:2 both are good. 
                        
                    2.  we divide the (1.1) first part in 2:3. img 19.
                        2.1 First part will contain  9 8
                        2.2 Second part will contain 7 3 6
                        
                    3.  we divide the (1.2) second part in 2:3. img 20.
                        3.1 First part will contain 4 1
                        3.2 Second part will contain 5 0 10
                        
                    this again dividing the problem into sub problems and so on.
                        
                        from the first step to third step 'we had a big array, we divide into two parts' now we have to sort these two parts seprately. "it can look likes we use the recursion" img 20.
                        every recursion has base case. so what is the smallest input we have for which we already know the ans what is the base case for us.
                            "Single element in the array".
                            means , if we have a array of one length, it is already sorted we can say.
                    so divide till that only one element in the array. 
                    img 21. these are teh sub problem which we know the ans.
                    now we have to simply merge that together.
                    
                    
                    Merging the array:-     this is the Conquering part we are doing.
                        1.  3,6 will merged as [3 6]. img 22.
                        2.  7 will merged with [3 6] in the sorted order as [3 6 7]. img 23.
                        3.  9,8 will merged as [8 9]. img 24.
                        4.  8,9 will merged with [3 6 7] as [3 6 7 8 9]. img 25.
                        
                        here, when we are merging merging ..., this is same as we did merging two sorted array into one sorted array. 
                        the smaller subparts (1 2 3 4) we have sorted, now combine that sorted parts into one part. same thing do in right side.
                        
                Coding steps:-
                    1.  array A, now at every step we don't look at the complete array, we look at the sub part of the array. initially start_index=0, end_index=N-1. 
                        void sort(A,start_index, end_index)
                    
                    2.  What is the condition to know if array has one element ?
                        if(start_index == end_index)    it means we are looking at only one elements in the array.                                                  // BASE CASE
                            return                      nothing to do in that case, simply return.
                    
                    3.  If it is not the case then find middle element.
                            mid = (start_index + end_index) / 2
                    
                    4.  Simply apply the first sum of the array, which is from starting till middle index.                                                          // LEFT HALF (means sub problems that we are solving)
                            sort(A, start_index, mid)
                    
                    5.  then apply the sorting in the second element of the array which is mid+1 till end index.                                                    // RIGHT HALF (means sub problems that we are solving)
                            sort(A, mid+1, end_index)
                            
                    6.  once the left half & right half are sorted then we merge it. so we write the merge function. we have to merge the left half & right half.   // Conquer Part (means merging the two subproblems)
                            merge(A, start_index, mid, end_index)        here no need to pass mid+1 as parameter becoz mid & mid+1 will taken care.
                            
                            Disclamer:- merge(A, start_index, mid, end_index)  this function is actually the merge two sorted array. so both the code are same. img 32.
                    
                    There are some divide steps going on. like at every steps divide into sub problems till reach one.
                        means at every step, the total array size N being reduced N/2 means left half become N/2, right half become N/2.
                        again next step, the subproblem become N/4 means left half become N/4, right half become N/4.
                        .
                        .
                        .
                        then eventually after some k steps, subproblem become N/2^k which should equal to 1.
                        so total no. of steps will basically the (logN)         Mean N will become, equal to 2^k which implies k will become logN. img 27. this is we can say total no. of levels that we can having.
                            like 4 times we are doing the divide part, img 28. if 4 times we are doing divide part then 4 times we have to do merge part also. img 29. 
                            so, if logN steps are there for divide then logN steps for the merge part also.
                        
                        Ques:-  To merge one Complete level What is the TC ?
                        Ans :-  
                                    let say, if we picking up these parts img 30. for one level. 
                                        like:-
                                            even though we are merging these two 8,9  3,6,7 seprately. it is 5 elements.    we are merging these two 1,4  0,5,10 seprately. it is 5 elements.  
                                            so merging this part (8,9  3,6,7) takes O(5) & this part (1,4  0,5,10) takes O(5), which is O(10) which is basically size of the array A. 
                                            therefore merging only one level completely takes O(N) TC.  see in pdf.
                                            
                                            basically we are doing merge at level, where N/2 elements, it will take O(N) TC.
                                            similarly when we have N/4 elements, (here we are merginng these two seprately, these two seprately img 31.) but ultimately total no. of element we are travelling is O(N) TC.
                                            so for next level it is O(N). 
                                            
                                   so for 1 level TC is O(N), for next level it it O(N), so for k levels it continue to be O(N).        
                                   total TC = O(N * log N).     
                    
                    Ques:-  Merging two sorted sorted array into one, will take how much time ?
                    Ans :-  TC = O(N), SC = O(N).       // Rercusion Space is K=logN. img 31. so finally the SC = O(N) becoz recursion space is smaller.
                            
                    Code:-
                             img 26.       
                ------------------------------------------------------
                
                Alternate Way:-
                    let say, we are not dividing into two halfs.
                        like:-
                                                     N elements
                             pick 1 element seprately        pick N-1 seprately     // so the 1 element is base case, it's ok.
                                  again pick 1 element seprately        pick N-2 seprately
                                              again pick 1 element seprately        pick N-3 seprately
                                                                                    .
                                                                                    .
                                                                                    .
                                                                                    .
                                                                                    N-k = 1 eventually, which implies k will actually equal to N-1.      // k levels we have to do this.
                                                                                                        now, k=N-1 then over all TC is O(N^2). it is very high becoz the divide part has lots of divide so the number of merges also high.
                                                                                                        therefore N times we are dividing, N times we are merging & each level merging take N times.
                                                                                                        so, O(N^2). that's why we divide into two parts
                    
                    Pending:-   due to don't completed the recursion relationship so rewatch from 01:22:00 to 01:24:00         
                
                In Java, Collection.sort has implementation of merge sort internally. but not all languages.                          

```
 ### Given an integer array, count the number of inversion pairs in the array, count the number of inversion pairs in the array.
1.  inversion pairs :-  (i,j)       **i<j & A[i] > A[j]**
``` 
       0 1 2
    A=[8 3 4] 
        pairs:- (0,1) (0,2) 
        Ans = 2
        
       0 1 2 3 4 5 
    A=[4 5 1 2 6 3]
        pairs:- (0,3) (0,2) (0,5) (1,2) (1,3) (1,5) (4,5) 
        Ans = 7
       
       0 1 2 3 4
    A=[4 4 4 4 4]
        Ans = 0
        
    
    Bruteforce way:-
                "for all i, j check for inversion".     
                TC = O(N^2)
                SC = O(1)
                
    Merge Sort:-    (Unsorted array)
           0 1 2 3 4 5 
        A=[4 5 1 2 6 3]     
        
        Divide Step:-
                first we divide into two parts.
                       4 5 1 2 6 3
                 4 5 1    |     2 6 3
                again divide two parts
                 4 5  |  1       2 6  |  3   
                again divide two parts
                 4  |  5       2  |  6   
        
        Merging Step:-
            when we do merging on these parts 4  |  5.      first we are selecting the element from left side that is 4. so 4,5 will remain same becoz 4<5.
                after merged:-  [4 5]
            
            when we do merging on these parts 2  |  6.      now we are selecting the element from left side that is 4. so 2, 6 will remain same becoz 2<6.
                after merged:-  [2 6]
           
            when we do merging on [4 5] with the element 1.  now i pointer & j pointer are at 4 1 (Two Pointer approach).
                i=0 j=2
                we will select the j element, it means there are two elements on left side which are greater than element 1 & which are forming conversion pair. so we have inversion count = 2.    index are (0,2) (1,2) these two case where i<j & A[i] > A[j]. img 33.
                after merged:-  [1 4 5]     inversion-count=2.  (0,2) (1,2)
            
            when we do merging on [2 6] with the element 3.  now i pointer & j pointer are at 4 1. (Two Pointer approach).
                i=3 j=5
                    2<3 so we take 2 as it is. (as long as we are taking the element from left side then we no need to worry). img 34.
                now i increase, compare 3 & 6, when we take element 3  then the element 6 is bigger than element 3. so it is part of inversion pairs. (4,5).
                i=4 j=5
                after merged:-  [2 3 6]     inversion-count=2.
            
            when we do merging of these two array [2 3 6] with the array [1 4 5].  now i pointer & j pointer are at 1 2. (Two Pointer approach).
                whichever is smaller will take it up. & (as long as we are taking the element from left side then we no need to worry) means i pointer. img 35.
                 i & j elements.
                 1 & 2 so [1] then increment the index i. 
                 4 & 2 so [1 2] then increment the index j. when we are taking up index j, it means two elements are bigger in left side element 4 5.   so two more inversion here. (0,3) (1,3)
                 4 & 3 so [1 2 3] then increment the index j. when we are taking up index j, it means two elements are bigger in left side element 4 5.   so two more inversion here. (0,5) (1,5)
                 4 & 6 so [1 2 3 4] then increment the index i. here we are taking elements from left side.  (as long as we are taking the element from left side then we no need to worry).
                 5 & 6 so [1 2 3 4 5] then increment the index i. here we are taking elements from left side. (as long as we are taking the element from left side then we no need to worry). now i is complete. so take the element from right side.
                 so [1 2 3 4 5 6].
                 
                 while doing the merge sorting we have count = 7.
                 Ans=7.
            
            Simply do one thing.    
                'sum of the No. of remaining elements in left part, if an element from right part is selected'  
                    
                    remaining elements we find like this:- (if total no. of elements in left half is) N - i (current index).    let say, [1 4 5] elements are in left side, currently i=1 so 3-1 = 2 elements are remaining.
                
                if there are equal scanerio then take element from left side.
                 so the exactly same code is working (merge two sorted array) here. becoz there we are taking element from left side (B[i]<= C[j]). 
                 
            
            Code:-  
                img 36.
                
                
                
    Merge Sort:-    (Sorted array)  
        In unsorted array, we are finding the ans while sorting the array.
        here, we have sorted array then we have finding the ans. 
           0 1 2 3 4 5
        A=[4 5 1 2 6 3]
        
        first we sort the array.
           0 1 2 3 4 5
        A=[1 2 3 4 5 6]
        
        left side element is bigger than the right side element. i<j & A[i] > A[j]
        if we look at the indexes. img 37.
        
        Index diff is,          {Original index - sorted index}
            In the                      original array              sorted array                   
            original array              index                       index 
              element are:-               is:-                        is:-
                    1                      2          -                 0                       2
                    2                      3          -                 1                       2
                    3                      5          -                 2                       3
                                                                                ----------------------------------
                                                                                                7 Ans.
                                                                                ----------------------------------  img 37.
        
        if we do the reverse then we will get the same ans. but we can't take these elements. we consider 4 5 6 elements. img 38.
            {sorted index -  Original index}
        
        Note:-  we will take into consideration only "the element which is giving the +ve difference".  
                    like:-
                        when we do {Original index - sorted index} then we are taking care of element 1 2 3 so we get positive results. if we take element 4, index of orginal array is 0 - index of sorted array is 3 = -3. img 39.
                so we have to do where it is giving the +ve result.
                           
        Ques:-  What actually we are doing ?
        Ans :-  In the original array, element 1 is at index 2 & In the sorted array, element 1 is at index 0. 
                
                that means In the original array, there are two element on the left of element 1 which are actually bigger.
                                                    ||
                if we have the array A.
                    A=[some elements _ _ _ 1 _ _ _ few more elements]         
                    A=[1 _ _ _ some elements _ _ _ few more elements]         now in the sorted version, element 1 is at index 0. 
                    
                    if 1 is the smallest element then we can say these some elements are smaller than 1.
                    
                    rewatch again. this if we want but it is not recommended to do, the simple way to solve this problem is this Merge Sort:-    (Unsorted array).
```
### Stability is basically **Relative order of equal elements should not change**.
``` 
    When we do any sorting algorithm we have to make sure that equal elements. 
    let say, element 8 is on left side & element 8 is on right side.
    after sorting also the left side element remain on left side & right side element remain on right side. means the equal elements relative order  will not change.
    
    Ques:-  Why Stability is Important ?
    Ans :-  
            Real world example:-
                let say, there are 10 people who want to caught the flight.
                 1 
                 2
                 3
                 4
                 5
                 6
                 7
                 8
                 9
                 10
                 they are actually standing in the line, they want to jump in the flight. 
                 now the airline company says we will give the priority to business class passangers. so whoever the business class passanger should come first (move ahead in the queue). 
                 person no. 2 5 6 & 9 are the business class passangers, if airline company says 'these 4 people are equally important' so all of them come forward.
                 if the persons are in the standing in the particular order (above) in which person 1 is almost about to bought the flight but becoz of business class priority these 4 people will bought the flight. img 40.
                 
                 if it is announced & suddenly the person 9 run & move to ahead & then enter the flight. then we can say it will create a conflict becoz person 2 5 & 6 will fight with person 9. img 41.
                    person 2 was about to caught the flight so the person 2 should be the first one to enter so Priority 1. then person 5 should be the one to enter so Priority 2. then person 6 should be the one to enter so Priority 3.
                    then person 9 should be the one to enter so Priority 4. once its done then airline company says now people who have the seat no. between 1 to 5 you can come so person 3, person 4 & person 8 have their seat in 1 to 5. 
                    they are equally important so these people gets the priority in the order in which they are standing. so the priority is Priority 5, Priority 6, Priority 7. & now remainig people can enter in the flight. img 42.
                    this is the final order in which people are entering. beocz for the airline company, 
                        person 3 4 8 have equal priority.
                        person 2 5 6 9 have equal priority.
                 so if these 4 people are equally important then the order should remain same.
                 
                 therefore "Whenever we are changing the order & their are equal elements" we have to maintain the relative order.
    
    How we will maintain a stability while solving in array. 
        "If elements are equal, compare index" becoz index can never be the equal.
        so based on the index we can descide which element should be on right side or left side.                                                           
```