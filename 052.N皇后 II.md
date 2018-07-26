# N皇后 II
## 问题描述
给定一个整数 n，返回 n 皇后不同的解决方案的数量。
## 解决方法（回溯法）
```java
class Solution {
    private int count=0;
    public int totalNQueens(int n) {
        int[] CollumnIndex=new int[n];
        for(int i=0;i<n;i++)
            CollumnIndex[i]=-1;
        Permutation(CollumnIndex,0);
        return count;
    }
    public void Permutation(int[] CollumnIndex,int row){
        if(row==CollumnIndex.length){
            count++;
        }else{
            for(int col=0;col<CollumnIndex.length;col++){
                if(isRight(CollumnIndex,row,col)){
                    CollumnIndex[row]=col;
                    Permutation(CollumnIndex,row+1);
                    CollumnIndex[row]=-1;
                }
            }
        }
    }
    public boolean isRight(int[] CollumnIndex,int row,int col){
        for(int i=0;i<row;i++){
            if(col==CollumnIndex[i]||Math.abs(row-i)==Math.abs(col-CollumnIndex[i])){
                return false;
            }
        }
        return true;
    }
}
```
