# 73. Set Matrix Zeroes <leetcode>

### **Problem** 
- Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's, and return the matrix.
- You must do it in place.
- Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]  ------>    Output: [[1,0,1],[0,0,0],[1,0,1]]
- Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]].  ------>   Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
    
    
### **Solution**
- We can use first element of each row/column as flag indicator for that row/column. It means if we make first element as 0 whole row/column will be set to zero.
- logic will be if matrix[i][j] = 0 then matrix[i][0] (first element of row i) and matrix[0][j] (first element of column j) should be set to 0.
- track of every row will be seen through first element of row. track of every column will be set by first element of column. Problem arises for matrix[0][0] element, matrix [0][0] will keep track of row 0 but what about column 0 . therefore we will use col0 for tracking first column. Try to do dry run will all row elements as 1 and first column has 0 on any >=1 position. e.g. [[1,1,1],[0,1,1],[1,1,1]] .  
- In first iteration set all flags to zero with logic described in point 2.
- In second iteration set zeros. As first element is used as flags, start second iteration from last m-1,n-1 position.
- Handle first cloumn separately.
- Main thing to handle is that element zero act as flag for row as well as column that why we need to have col0.

``` cpp
    
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        
        // flag for column 0
        int col0 = 1;
        int R = matrix.size();
        int C = matrix[0].size();
        
        // use first element of each row and column as flag
        for(int i=0;i<R;i++){
            // update flag for column 0
            if(matrix[i][0] == 0){
                col0 = 0;
            }
            // for column start with j=1
            for(int j=1;j<C;j++){
                // if i,j element is zero menas that row and column should be zero , so set i,0 and j,0 to 0.
                if(matrix[i][j] == 0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }    
            }
        }
        
        // for 2 iteration start from last because first row and column is used as flag, update them at last
        for(int i=R-1;i>=0;i--){
            // update till second column
            for(int j=C-1;j>0;j--){
                if(matrix[i][0] == 0 || matrix[0][j] == 0){
                    matrix[i][j] = 0;    
                } 
            }
            // update first column explicitly
            if(col0 == 0){
                matrix[i][0] = 0;        
            }
        }
    }
};

```
