# 73. Set Matrix Zeroes <leetcode>

Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's, and return the matrix.
You must do it in place.

  '''
  class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int col0 = 1;
        int R = matrix.size();
        int C = matrix[0].size();
        
        for(int i=0;i<R;i++){
            if(matrix[i][0] == 0){
                col0 = 0;
            }
            for(int j=1;j<C;j++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }    
            }
        }
        
        for(int i=R-1;i>=0;i--){
            for(int j=C-1;j>0;j--){
                if(matrix[i][0] == 0 || matrix[0][j] == 0){
                    matrix[i][j] = 0;    
                } 
            }
            if(col0 == 0){
                matrix[i][0] = 0;        
            }
        }
    }
};
  '''
