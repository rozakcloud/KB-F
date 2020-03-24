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

Contoh dari algoritma BFS
![F0hfQ](https://user-images.githubusercontent.com/61219666/77388940-2c271d80-6dc4-11ea-8004-471f64f0ff6c.gif)

Step:
1. node 1 dikunjungi terlebih dahulu
2. lalu mengecek ke tetangganya yaitu 8, 5, 2 dan queue 8, 5 dan 2
(queue : 8 5 2)
3. mengecek queue pertama yaitu 8, mempunyai 3 tetangga yang belum di cek yaitu 6, 4 dan 3
(queue :8 5 2 6 4 3)
4. mengecek tetangga dari 8 yaitu 6, 4, 3. dan queue 6, 4 dan 3. lalu unqueue 8
(queue :5 2 6 4 3)
6. mengecek tetangga dari 5, namun 5 tidak mempunyai tetangga lagi, maka unqueue 5
(queue :2 6 4 3)
7. mengecek tetangga dari 2, yaitu 9, lalu queue 9 dan unqueue 2
(queue :6 4 3 9)
8. mengecek tetangga dari 6, yaitu 10 dan 7, lalu queue 10 dan 7, dan unqueue 6
(queue :4 3 9 10 7)
10. mengecek tetangga dari 4, 3, 9, 10 dan 7 namun node tersebut tidak mempunyai tetangga lagi, maka unqueue 4, 3, 9, 10, 7
(queue :-)

untuk penerapan pada 8 puzzle, kita mencari seperti contoh diatas, bila pada pertengahan step itu sudah ditemukan node final yang kita cari maka langsung di outputkan.
