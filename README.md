## Binary Search
1.  means **We divide the Search space in Two part** that's why we called as Binary Search.
``` 
    Given:- There are some integers which are on Ascending order 
            like:-
                    _________8___________           Ascending ordered data.         Target = 15, that we are looking for. 
                         in this data we know only one element that is 8.
                         so, if data is in ascending order & we know the element 8 then we can think like "8 is less than 15. so all the things on left side of 8 will also be less than 15. 
                            the right part of the 8 is the place where we have to search for the target" (Search Space).
```
### Problem0:-  Given a sorted array of distinct elements, find index of a given target.    
``` 
    A = [1 3 5 7 9 10 11 13 15 17 19 30 35 40]
         0 1 2 3 4  5  6  7  8  9 10 11 12 13   
        Ques:- Which element we should start first ? 
        Ans :-  Mid element
                    if we start from first element means we compare first element with target & we got to know that first element is smaller than target then we have to travrse all the remaining elements which is greater than first element. img 1
                    if we start from last element means we compare last element with target & we got to know that last element is greater than target then we have to travrse all the remaining elements which is less than last element. 
                    if we start from any random location then also there is some part of the data which is discarded & still the search space is larger side. img 2.
                    if we make sure that discarded data should be maximise so the search space is smaller then "Always starts from Middle ELement".
                    so, search space size will reduce from N to N/2. and so on. img 3.
                    TC = o(log N)
        
        Bruteforce Way:-
                "Traverse all the element & compare with target & return the index".            ==>     Linear Search 
         l                                  r
    A = [1 3 5 7 9 10 11 13 15 17 19 30 35 40]
         0 1 2 3 4  5  6  7  8  9 10 11 12 13               l to r is the entire search space. mid element is smaller or larger that we check below.
                                                        
               l    |     r     |   mid                     |
          ----------|-----------|---------------------------|------------                                                        // initally 0 to 13 entire array is the search space. so we start comparing from index 6.
               0    |     13    |    (0+13)/2   =   6       |   A[6] element is smaller than the target so we will discar the left part the A till mid element.  & we search in right part means update the left pointer to index mid + 1. l = mid+1. now search space is from index 7 to 13.
               7    |     13    |   (7+13)/2    =   10      |   A[10] element is greater than the target. means ans will be left side. so we update the right element from mid - 1.
               7    |     9     |   (7+9)/2     =   8       |   A[8] element is smaller than the target & we search in right part means update the left pointer to index mid + 1. after this l & r at same place.
               9    |     9     |   (9+9)/2     =   9       |   A[9] element is match with target.      // assume if target does not match then return target does not exist becoz search space is over now.
         
         Ans = 9.    
    Code:-  Standard Binary Search Algorithm.       this will followed all the binary search question & make solution easy.
            l = 0, r = (N-1)        // defining search space.           "In every question, the complete array is not search space, we have to define the search space in some problems see in next video", like what we are looking in.
            while (l<= r)           // while the search space exists we traverse.
            {
                mid = (l+r)/2       // or we can do like this:- l+(r-l)/2       // there can be situation where l & r can large values, in this case l+r can overflow so we prefer "l+(r-l)/2" to resolve overflow issue. as of now we deal with idex so l+r is fine.
                if(A[mid] == target) // check if mid is ans
                {
                    return mid;
                }
               if(A[mid] < target)  // to know wether we go left side or right side.
               {
                l = mid+1;
               }
               else
               {
                    r = mid-1;
               }
            }
           return -1    // indicate that ans is not present.     
         
    TC = O(log N)
    SC = O(1)                 
```
### Problem1:-  Given a sorted array of elements, find first index of a given target.
``` 
    A = [2 2 5 5 5 5 8 10 10 13 13 13]
         0 1 2 3 4 5 6  7  8  9 10 11           Target = 5      Ans = 2 becoz, target can present at multiple location but at index is the first location.
        
        Solution1:- "Find any location of target & iterate on left side to find first index".       Approach is fine but issue with TC. 
                    A = [2 2 2 2 2 2 2 ............................2 2 2 2 2]       Target = 2
                    
                    mid = 2.
                    mid == target   ==> so we have to go on left side & keep on travelling on left side to find the first index.
                    TC = O(N)   SC = O(1)

                    conclusion:-    it is as good as iterating the complete array.

        Solution2:-         (there are multiple ways to find the ans but we can follow the above binary search steps)
        
                    l start from 0.
                    r start from N-1.
                    mid start from (l+r) / 2.
                    now, mid == target.     (now, we have to check wether mid is ans or not, then descide wether go left side or right side)
                    Ques:-  How to know wether mid is my ans ?  is this first index of target ?
                    Ans :-  "If we just check the Left Element from the mid" means previous of the mid element is also equal to target then current mid is not the first index of the target. img 3.
                            then update right boundary.
                            see dry run in pdf.
                            
                    Code:-  Binary search algo to find the first index of the element.
                        l = 0;
                        r = N-1;           
                        while (l<=r)
                        {
                           if(A[mid] == target && A[mid] != A[mid-1])       ==> it will throw index out of bound error, when target found at index 0;
                        }
                        // update code
                        while (l<=r)
                        {
                           if(A[mid] == target && (A[mid] == 0 || A[mid] != A[mid-1])                   // HW:- f(A[mid] == target && (A[mid] == 0 || A[mid] != A[mid+1]) to know wether it is last index or not.   now corner case will be N-1 index that we have to handle.
                            {
                                return mid;
                            }
                            if (A[mid] < target)
                            {
                                l = mid+1;
                            }
                            else        // here we have to handle current element should be greater || equal to target. means if current element is greater then we go left side || if current element is equal to target then we go left side to find first index. 
                            {
                                r = mid-1;
                            }
                        }   
                    TC = O(log N)           // just some condition we solve the question. 
                    SC = O(1)
                    
                    HomeWork Ques:- What is the best TC to find the count of elements with value x in the sorted array that can contain duplicate elements using binary search.     ==>     O(log N)
                        re watch video, 00:49:49  
                        -   we have done the binary search to find the first index which match with target.
                        -   we have to write binary search to find the last index which match with target.      Hw.
                                when we finding last index then we go to right side (of the first index).       index 2             TC = O(log N)               frist index is L.   
                                Once we know first index & last index.                                          index 5.            TC = O(log N)           last index is R.       //  now if current element is less than || less than equal to target, we have to go in right side. 
                                then we find count of elements.
                                How ?
                                if we know the First index till Last index all elements are five then we can do, 
                                    R-L+1.                                                                                    Total TC = O(log N) 
```
### Problem2:-   Given a sorted integer array where every element appears twice except for one element, find that unique element.       (already did in Bit Manipulation Basics)
``` 
   A = [2 2 5 5 8 10 10 13 13 18 18]        Ans = 8.
        
        Sol1:-  "Ans = for all elements take XOR".
                TC = O(N)
                SC = O(1)

        If we forgot the XOR then how we can find the ans in same TC & SC. 
        
        Sol2:-   Linear Search.
                 "Iterate the array from left to right, becoz the array is sorted, all the elements are twice they adjecent to each other (means near), only unique element will not be having any neighbour equal to itself".
                 means for current element we have to check left side & right side, if any of them are not equal then that is the Ans.
                 TC = O(N)
                 SC = O(1)
                 Code:-
                        for all A[i] ==> if(A[i] != A[i-1] && A[i] != A[i+1]
                                l=0, r=N-1                          //  Define Search space.
                                while(l<=r)
                                {
                                    mid = (l+r)/2;
                                    if(A[mid] != A[mid-1] && A[mid] != A[mid+1])        // check if mid is answer.
                                }
                                                // till here corner cases will create problems like, img 4.
                                                // solving the these 3 corner cases that show in img 4.
                                
                                l=0, r=N-1                          //  Define Search space.
                                while(l<=r)
                                {
                                    mid = (l+r)/2;
                                                                            // check if mid is answer.    other way to handle corner case.   we can handle it outside the code where we seprately check the first & last case.
                                    if ((mid == 0 || A[mid] != A[mid-1])     // if we are at first index then no need to check left neighbour so we check right neighbour if current & right neighbour are not same then cur is the ans.        
                                            &&  
                                    (mid == N-1 || A[mid] != A[mid+1]))     // if we are at last index then no need to check right neighbour so we check left neighbour if current & left neighbour are not same then cur is the ans.          &    if mid is 0 & N-1 that means only one element is present in the array.
                                     {
                                            return A[mid];                  // Ans part.
                                     } 
                                            // Decide when to go left/right.        one of the way is count of element                                   
                                  // pending.  
                                             
                                
                             0 1 2 3 4  5  6  7  8  9 10  
                        A = [2 2 5 5 8 10 10 13 13 18 18]        Ans = 8.
                            
                            -   If we standing at index 4 then we want to know that the current element is ans or not. that we can know by checking left & right neighbour is different. img 5.
                            -   if we standing at index 0 to 3 that means we have to figure out a way to go on the right side. img 6.
                            -   if we standing at index 5 to 10 that means we have to figure out a way to go on the left side. img 7.
                            
                            Observations:-
                                every elements appear in the pair. img 8.
                                there are a pattern. img 8
                                    Pattern:-   "On the left side of Ans, the equal elements are following this pattern = even --> odd (means even index followed by odd index. like index 0 is follow by index 1 || means first even then odd)"
                                                    but the pattern has changed as soon as there is single element (which does not have pair || unique element). after this
                                                "the equal elements followed the pattern = odd --> even (means odd index followed by even index. like index 7 is follow by index 8 || means first odd then even)". img 8.
                                    
                                    Summary:-   "The equal element pattern, even odd on left side of the ans, odd even on right side of the ans".     This will tell us that we should look for the ans in either left side or right side.
                                    
                            // continue code.
                                //   we have define the search space.
                                //   we have check that mid is the ans or not. if mid not the ans then we should check
                                    if(mid != 0 && A[mid] == A[mid-1]               // means if mid-1 & mid are equal  
                                    {
                                        if(mid % 2 == 0)        // if mid index is even index then the pattern is "odd --> even" then we should go in Left side. means going into left side is nothing but Updating the right boundary". 
                                            r = mid-1;
                                        else
                                            l = mid+1;
                                    }                         // this is condition when middle & mid-1 elements are equal 
                                    else                      // now when mid & mid+1 element are euql.
                                    {
                                            if(mid % 2 == 0)        // now mid is even iddex have to go for "even --> odd" means go on right side so update the left boundary.
                                                l = mid + 1;
                                            else            // means it is odd even pair then we have to go on left side so update the right side
                                                r = mid-1;  // then we have to go on left side so update the right side
                                                
                                    }
                                }
                                return -1;          // if we want 
                            
                            =   we are sure that elements exists in the pair so (mid, mid-1) will be equal or (mid, mid+1) will be equal becoz ans part has taken care above.       there is no other case.
                            
                            
                 Dry Run:-  
                             l      |       r       |       mid             |   Case
                        ------------|---------------|-----------------------|-------------
                             0      |       10      |     (0+10)/2  =   5   |   odd-->even    img 9.      // first we check that mid should not be equal to left & right neighbour. but mid is equal to right neighbour then we check mid index != 0 && mid element has == mid-1 element, it become false. then we go in else part & check Is Mid even index, No. then we go to else part & update the right boundary r= mid-1.
                             0      |       4       |     (0+4)/2   =   2   |   even-->odd               // watch video form 01:30:00 if require.
                             3      |       4       |     (3+4)/2   =   3   |   even-->odd
                             4      |       4       |     (4+4)/2   =   4   |   answer.
                
                 TC = O(log2(N))
                 SC = O(1)
```
### Problem 3:-  Given an increasing-decreasing array with distinct elements. find Max element.
``` 
    img 10.
    Scanerio 1:-
        -   if mid element is maximum that means mid-1 & mid+1 elements will be smaller.
    Scanerio 2:-
        -   if we are at increasing sequence then we have to go on right side, to find the ans. because it is increasing & then decreasing means to find the max we have to go to right side becoz it is increasing.
    Scanerio 3:-
        -   if we are at decreasing sequence that means mid+1 is smaller, mid-1 is greater so we have to go on left side, to find the ans.
    
    Code:-
            l=0,    r=N-1
            while(l<=r)
            {
                mid = (l+r)/2;
                                // to know wether the mid is ans or not we compare left & right element.    What if the element in the array are only in increasing part,       What if the element in the array are only in decreasing part,       What if the single element is present in the array.
                if ((mid == 0 || A[mid] > A[mid-1]) 
                        &&  
                (mid == N-1 || A[mid] > A[mid+1]))     
                        return A[mid];                  // if mid is the ans then this if condtion will take care.
                 }
                      // Decide when to go left/right.    
                    //  do we really need to compare with both the data like (mid-1 with mid) (mid+1 with mid) both. if we are at increasing sequences. ==>   No, if we already know that mid element is not the ans then we  don't have to check both case, becoz if (mid-1 with mid) part is increasing then everything is increasing, if (mid with mid+1) part is increasing then everything else is increasing then why we will check.   
                if(mid == 0 && A[mid] > A[mid-1]        // means it is increasing order.  if first element is the ans or not the ans then we go right side.     so updating the left boundary, means we have to go on right side.  
                {
                        l = mid+1;
                }
                else
                {
                        r = mid-1;
                } 
            }
            return -1      // not required, becoz ans will be return.
            //   this is also know as peak element problem.

    TC = O(log2(N))
    SC = O(1)



```
### Problem 4:-   Given a random array (unsorted) with distinct elements, find any one local minima in the array.
``` 
    Local Minima:-  whenever there is an input array, there can be increasing decreasing elements. means it random order array, where the dips in the array (pointed, img 11) are called local minima.
                    the corner elements are also local minima becoz either one neighbour is present or both the neighbour is present. img 11.  

    Sol1:-  Finding Smallest element in the array.  means Smallest element will be the Global minima, Global Minima is anyways a Local Minima.  (Correct Solution)
            TC = O(N)
            SC = O(1)
    
    There can be diff diff cases.
        -   we are at the element, which is the ans. like mid-1 & mid+1 both element are bigger than mid element, in that case mid is the ans. img 11.
            Corner case:-
                    if ans is the starting element of the array & next element is bigger then this is the ans.
                    if ans is the last element of the array & left side is bigger then this is the ans. 
        
        -   if we are at decreasing sequence in that case, 'there may be possible that left side(mid-1 side) has any local minima becoz it can decreasing-increasing(img 12), not gurantee', 'on the right side the data can be decreasing to the certain point, either it will stop decreasing from that point or it will increasing from that point in both the ways this is the ans(green color dip)', gurantted we get local minima. img 13
        
        -   if we are at increasing sequence in that case, 'on left side data will going down till certain point either it will stop or it will start going up.' img 14
    
    Think:-
        Ques:-  if the mid element is greater than mid-1 & mid element is greater than  mid+1 element then where we get at least one local minima ?
        Ans :-  both side.
                Explain:-
                        if we actually standing at peek, {In Binary Search we can go anywhere, either go left or right not both the side} means if we go left side(mid-1 side) then data is decreasing at certain point from that point either it will stop decreasing or it will start increasing. 
                            if we go right side(mid+1 side) then data is decreasing at certain point from that point either it will stop decreasing or it will start increasing. img 15.
                        at least one local minima need to be return.
        
        Finding peek element is base for the question.
        
        Code:-
            l=0,    r=N-1
            while(l<=r)
            {
                mid = (l+r)/2;
                                
                if ((mid == 0 || A[mid] < A[mid-1]) 
                        &&  
                (mid == N-1 || A[mid] < A[mid+1]))     
                        return A[mid];                                          // handling Ans case
                 }      
                      // Decide when to go left/right.    
                       
                if(mid != 0 && A[mid] > A[mid-1])   // increasing sequence    // handling increasing case  
                {
                         r = mid-1;              // now we will go on left side. 
                }
                else                            // decreasing sequence      // handling decreasing case         // here, A[mid] < A[mid-1]
                {
                        l = mid+1;              // else we will go right side.              // here, mid == 0                       // if required watch doubt session of binary search 1
                } 
            }
             return -1      // not required, becoz ans will be return.  
                            // mind blowing thing:- we can go any side.
             
                    Ques:-  Where we are handling peek element (green color circle), img 15. in the above code. if part or elese part ?
                    Ans :-  
                            Explain:-
                                    we are checking the mid element & mid-1 element, we are not checking the mid+1 element so if the mid+1 element is increasing from mid element or decreasing from mid element, we don't care becoz we are going on left side only. means if the peek element we still go on left side or if it is increasing then also we go on left side. basically we not checking mid+1
                                        "Becoz the ans will be present on left side" so we can go on left side. that's why we descided that if peek element then go left side. if we want we can go right side also that is also fine.
        
        TC = O(log2(N))
        SC = O(1)
```




