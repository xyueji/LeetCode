# N皇后
## 问题描述
n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。
## 解决方法
### 方法一
声明一个长度为n的数组CollumnIndex，初始化CollumnIndex为0`n-1的数，CollumnIndex[i]表示第i行上存着第CollumnIndex[i]列，由于CollumnIndex[i]的值各不相同，所以全排列数组代表着皇后在不同行、不同列的所有情况，然后去除在对角线上的情况（i-j==CollumnIndex[i]-CollumnIndex[j]||i-j==CollumnIndex[j]-CollumnIndex[i]).
```java
class Solution {
    private List<List<String>> lrs=new ArrayList<>();
    public boolean isRight(int[] ColumnIndex){
        for(int i=0;i<ColumnIndex.length;i++){
            for(int j=i+1;j<ColumnIndex.length;j++){
                if(i-j==ColumnIndex[i]-ColumnIndex[j]||i-j==ColumnIndex[j]-ColumnIndex[i]){
                    return false;
                }
            }
        }
        return true;
    }
    public List<List<String>> solveNQueens(int n) {
        int[] ColumnIndex=new int[n];
        for(int i=0;i<n;i++)
            ColumnIndex[i]=i;
        Permutation(ColumnIndex,0);
        return lrs;
    }
    public void Permutation(int[] ColumnIndex,int begin){
        if(begin==ColumnIndex.length-1){
            if(isRight(ColumnIndex)){
                List<String> list=new ArrayList<>();
                for(int i=0;i<ColumnIndex.length;i++){
                    StringBuilder sb=new StringBuilder();
                   for(int j=0;j<ColumnIndex.length;j++){
                        if(j==ColumnIndex[i]){
                            sb.append("Q");
                        }else{
                            sb.append(".");
                        }
                   }
                    list.add(sb.toString());
            }
                lrs.add(list);
            }
        }else{
            for(int i=begin;i<ColumnIndex.length;i++){
                int temp=ColumnIndex[i];
                ColumnIndex[i]=ColumnIndex[begin];
                ColumnIndex[begin]=temp;
                Permutation(ColumnIndex,begin+1);
                temp=ColumnIndex[i];
                ColumnIndex[i]=ColumnIndex[begin];
                ColumnIndex[begin]=temp;
            }
        }
    }
}
```
### 方法二（回溯法）
声明一个数组ColumnIndex，初始化数组为-1，ColumnIndex[i]表示第i行的位置，遍历第i行的每列，当第i行满足规则赋值ColumnIndex[row]=col并往下一行进行，否则赋值ColumnIndex[row]=-1（代表这个位置不满足条件），直到row到最后一行，则这时的ColumnIndex为一种符合情况。
```java
class Solution {
    private List<List<String>> lrs=new ArrayList<>();
    public boolean isRight(int[] ColumnIndex,int row,int col){
        for(int i=0;i<row;i++){
            if(col==ColumnIndex[i]||Math.abs(row-i)==Math.abs(col-ColumnIndex[i]))
                return false;
        }
        return true;
    }
    public List<List<String>> solveNQueens(int n) {
        int[] ColumnIndex=new int[n];
        for(int i=0;i<n;i++)
            ColumnIndex[i]=-1;
        Permutation(ColumnIndex,0);
        return lrs;
    }
    public void Permutation(int[] ColumnIndex,int row){
        if(row==ColumnIndex.length){
                List<String> list=new ArrayList<>();
                for(int i=0;i<ColumnIndex.length;i++){
                    StringBuilder sb=new StringBuilder();
                   for(int j=0;j<ColumnIndex.length;j++){
                        if(j==ColumnIndex[i]){
                            sb.append("Q");
                        }else{
                            sb.append(".");
                        }
                   }
                    list.add(sb.toString());
            }
                lrs.add(list);
        }else{
            for(int col=0;col<ColumnIndex.length;col++){
                if(isRight(ColumnIndex,row,col)){
                    ColumnIndex[row]=col;
                    Permutation(ColumnIndex,row+1);
                    ColumnIndex[row]=-1;
                }
            }
        }
    }
}
```
