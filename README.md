# KB-F

# 1. N Queen (4 & 8)
Pada problem N queen ini digunakan algoritma backtracking, yaitu mencoba menaruh queen dimulai dari kolom atas kiri atau kolom pertama baris pertama, lalu kita mencoba menaruh queen lain dan di cek apakah ada yang saling melawan atau tidak. Jika saat kita menaruh queen dan tidak ada yang saling melawan dengan queen lain maka baris dan kolomnya akan dijadikan sebagai bagian dari solusi, bila pada hasil akhir tidak ditemukan hasil yang tepat karena masih ada queen yang saling melawan, maka akan di backtrack dan return false.

Fungsi untuk menaruh queen

    bool solveNQUtil(int board[N][N], int col) 
    { 
    /* base case: If all queens are placed 
      then return true */
    if (col >= N) 
        return true; 
  
    /* Consider this column and try placing 
       this queen in all rows one by one */
    for (int i = 0; i < N; i++) { 
        /* Check if the queen can be placed on 
          board[i][col] */
        /* A check if a queen can be placed on  
           board[row][col].We just need to check 
           ld[row-col+n-1] and rd[row+coln] where 
           ld and rd are for left and right  
           diagonal respectively*/
        if ((ld[i - col + N - 1] != 1 && 
        
        
                  rd[i + col] != 1) && cl[i] != 1) { 
            /* Place this queen in board[i][col] */
            board[i][col] = 1; 
            ld[i - col + N - 1] = 
                          rd[i + col] = cl[i] = 1; 
  
            /* recur to place rest of the queens */
            if (solveNQUtil(board, col + 1)) 
                return true; 
  
            /* If placing queen in board[i][col] 
               doesn't lead to a solution, then 
               remove queen from board[i][col] */
            board[i][col] = 0; // BACKTRACK 
            ld[i - col + N - 1] = 
                         rd[i + col] = cl[i] = 0; 
        } 
    } 
  
    /* If the queen cannot be placed in any row in 
        this colum col  then return false */
    return false; 
    } 
Fungsi untuk mengecek apakah fungsi dari solveNQUtil mereturn false atau tidak

    bool solveNQ() 
    { 
    int board[N][N] = { { 0, 0, 0, 0 }, 
                        { 0, 0, 0, 0 }, 
                        { 0, 0, 0, 0 }, 
                        { 0, 0, 0, 0 } }; 
  
    if (solveNQUtil(board, 0) == false) { 
        printf("Solution does not exist"); 
        return false; 
    } 
  
    printSolution(board); 
    return true; 
    } 

# 2. 8 Puzzle BFS
Breadth First Search merupakan pencarian node tujuan dengan pencarian secara melebar, pertama kita mengunjungi node pertama lalu mengunjungi node yang bertetangga terlebih dahulu. Lalu mengunjungi node yang bertetangga dengan node yang telah dikunjungi.

![F0hfQ](https://user-images.githubusercontent.com/61219666/77388940-2c271d80-6dc4-11ea-8004-471f64f0ff6c.gif)
