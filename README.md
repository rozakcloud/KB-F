# KB-F

# 1. 8 Puzzle BFS
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

# 2. 8 Puzzle DFS
Depth-First Search merupakan algoritma penelusuran pada struktur pohon berdasarkan kedalaman terlebih dahulu, simpul ditelusuri dari root kemudian ke salah satu simpul anaknya(biasanya prioritas ke kiri), lalu dari simpul tersebut akan dicari terus sampai pada simpul ujung yang tidak mempunyai anak lagi. setelah penelusuran sampai ke paling bawah, maka penelusuran akan kembali ke 1 level diatasnya dan mencari anak lainnya yang belum di telusuri.
Contoh dari algoritma DFS:
![DFS](https://user-images.githubusercontent.com/61219666/80278302-53ed0680-871f-11ea-9a81-41087906a74f.png)
penelusuran dimulai dari root yaitu A
A-B-D-H-E-I-C-F-G-J-K-L

# 3. 8 Puzzle IDS
Iterative Deepening Search merupakan pengembangan dari algoritma Depth First Search, IDS menggunakan konsep penelusuran secara DFS dimulai dari limit 1. Saat solusi belum ditemukan makan pencarian dilakukan lah iterasi ke-2, pencarian kini limitnya bertambah menjadi 1 level menjadi limit 2, bila solusi masih belum ditemukan lakukan kembali iterasi ke-3 dengan menambah limit 1 level menjadi limit 3. Begitu seterusnya hingga ditemukan solusi yang dicari.

Contoh penelusuran dengan metode IDS:
![27857460-62fdcfb4-618f-11e7-89d2-661f304aa2dd](https://user-images.githubusercontent.com/61219666/80278697-a7148880-8722-11ea-85f1-2f7a9f373e03.png)

# 4. 8 queen
Pada problem N queen ini digunakan algoritma backtracking, yaitu mencoba menaruh queen dimulai dari kolom atas kiri atau kolom pertama baris pertama, lalu kita mencoba menaruh queen lain dan di cek apakah ada yang saling melawan atau tidak. Jika saat kita menaruh queen dan tidak ada yang saling melawan dengan queen lain maka baris dan kolomnya akan dijadikan sebagai bagian dari solusi, bila pada hasil akhir tidak ditemukan hasil yang tepat karena masih ada queen yang saling melawan, maka akan di backtrack dan return false.

Fungsi untuk menaruh queen
```c
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
```
Fungsi untuk mengecek apakah fungsi dari solveNQUtil mereturn false atau tidak
```c
    bool solveNQ() 
    { 
    int board[N][N] = { { 0, 0, 0, 0, 0, 0, 0, 0, }, 
                        { 0, 0, 0, 0, 0, 0, 0, 0, }, 
                        { 0, 0, 0, 0, 0, 0, 0, 0, }, 
                        { 0, 0, 0, 0, 0, 0, 0, 0, },
                        { 0, 0, 0, 0, 0, 0, 0, 0, }, 
                        { 0, 0, 0, 0, 0, 0, 0, 0, }, 
                        { 0, 0, 0, 0, 0, 0, 0, 0, }, 
                        { 0, 0, 0, 0, 0, 0, 0, 0  } }; 
  
    if (solveNQUtil(board, 0) == false) { 
        printf("Solution does not exist"); 
        return false; 
    } 
  
    printSolution(board); 
    return true; 
    } 
```  
# 5. 8 Puzzle Heuristics

Dalam program ini diminta untuk menyelesaikan 8 puzzle menggunakan metode heuristic 1 dan 2. Dimana penjelasan heuristic 1 dan 2 ada dibawah. Jika menggunakan heuristic 1 maka yang dilihat yaitu banyaknya grid yang menempati tempat yg salah, tetapi jika menggunakan heuristic 2 maka yang dilihat yaitu total keseluruhan jarak tiap grid yang menempati tempat yang salah terhadap posisi grid yang benar, atau sering disebut dengan manhattan distance.

Jadi dalam penyelesainnya kita mengeluarkan hasil setiap langkah puzzle dengan melihat penempatan grid yang salah kemudian dicari penempatan grid yang benar untuk mencapai final state yang diinginkan.

Dalam program ini, penyelesaian dengaan menggunakan tree, seperti pada gmbar dibawah nantinya.
```c
struct Node { 
	// stores the parent node of the current node helps in tracing path when the answer is found 
	Node* parent; 
	// stores matrix 
	int mat[N][N]; 
	// stores blank tile coordinates 
	int x, y; 
	// stores the number of misplaced tiles 
	int cost; 
	// stores the number of moves so far 
	int level; 
}; 
```

Kemudian setiap langkah pastinya memerlukan node untuk meletakkan grid nya, maka dari itu program dibawah ini untuk meyediakan node setiap langkah.
```c
Node* newNode(int mat[N][N], int x, int y, int newX, int newY, int level, Node* parent) { 
	Node* node = new Node; 
	// set pointer for path to root 
	node->parent = parent; 
	// copy data from parent node to current node 
	memcpy(node->mat, mat, sizeof node->mat); 
	// move tile by 1 position 
	swap(node->mat[x][y], node->mat[newX][newY]); 
	// set number of misplaced tiles 
	node->cost = INT_MAX; 
	// set number of moves so far 
	node->level = level; 
	// update new blank tile cordinates 
	node->x = newX; 
	node->y = newY; 
	return node; 
} 
```

Karena heuristic ini melihat posisi grid yang salah, maka fungsi program dibawah ini untuk menghitung banyak nya angka yang tidak sesuai dengan final state.
```c
int calculateCost(int initial[N][N], int final[N][N]) { 
	int count = 0; 
	for (int i = 0; i < N; i++) 
		for (int j = 0; j < N; j++) 
			if (initial[i][j] && initial[i][j] != final[i][j]) 
				count++; 
	return count; 
} 
```

Untuk bagian dibawah ini adalah pergerakan puzzle yang dimisalkan dengan `botton, left, top, right`
```c
int row[] = { 1, 0, -1, 0 }; 
int col[] = { 0, -1, 0, 1 }; 
```

Setelah itu, fungsi dibawah ini untu megecek apakah posisi grid dimana angka didalamnya sudah sesuai dengan final statenya.
```c
int isSafe(int x, int y) { 
	return (x >= 0 && x < N && y >= 0 && y < N); 
} 
```

Semua fungsi dijalankan dalam fungsi dibawah ini dimana untuk mengecek solusi penyelesaian menggunakan heuristic dengan initial awal puzzle yang dimasukkan kemudian final state yang diinginkan.
```c
void solve(int initial[N][N], int x, int y, int final[N][N]) { 
	// Create a priority queue to store live nodes of search tree; 
	priority_queue<Node*, std::vector<Node*>, comp> pq; 
	// create a root node and calculate its cost 
	Node* root = newNode(initial, x, y, x, y, 0, NULL); 
	root->cost = calculateCost(initial, final); 
	// Add root to list of live nodes; 
	pq.push(root); 
	// Finds a live node with least cost, add its childrens to list of live nodes and 
	// finally deletes it from the list. 
	while (!pq.empty()) { 
		// Find a live node with least estimated cost 
		Node* min = pq.top(); 
		// The found node is deleted from the list of live nodes 
		pq.pop(); 
		// if min is an answer node 
		if (min->cost == 0) { 
			// print the path from root to destination; 
			printPath(min); 
			return; 
		} 
		// do for each child of min, max 4 children for a node 
		for (int i = 0; i < 4; i++) { 
			if (isSafe(min->x + row[i], min->y + col[i])) { 
				// create a child node and calculate its cost 
				Node* child = newNode(min->mat, min->x, 
							min->y, min->x + row[i], 
							min->y + col[i], 
							min->level + 1, min); 
				child->cost = calculateCost(child->mat, final); 

				// Add child to list of live nodes 
				pq.push(child); 
			} 
		} 
	} 
} 
```

![8p](https://user-images.githubusercontent.com/52326074/77151801-52e60b00-6ac9-11ea-84f6-e27a66305731.png)

8-puzzle adalah puzzle yang ditemukan dan dipopulerkan oleh Noyes Palmer Chapman pada tahun 1870-an. Ini dimainkan pada kotak 3-oleh-3 dengan 8 blok persegi berlabel 1 hingga 8 dan kotak kosong. Tujuan Anda adalah mengatur ulang blok agar sesuai. Anda diizinkan untuk menggeser blok secara horizontal atau vertikal ke dalam kotak kosong. Berikut ini menunjukkan urutan langkah hukum dari posisi dewan awal (kiri) ke posisi tujuan (kanan).

8-Puzzle merupakan salah satu jenis permainan puzzle dimana kita harus mencapai goal puzzle dari initial puzzle yang diberikan. Untuk mencapai goal puzzle, 8-puzzle ini menyediakan satu grid kosong agar grid-grid lain disekitarnya dapat digerakkan. Sebagai contoh Inisial State dan Goal State dari sebuah puzzle adalah :

![8ph](https://user-images.githubusercontent.com/52326074/77028971-f9001b00-69cc-11ea-9301-6be95c8f1df1.PNG)

Pada pembahasan kali ini, saya ingin menyelesaikan puzzle ini dengan suatu algoritma, yaitu Algoritma Greedy, dengan menggunakan dua fungsi heuristik. Algoritma Greedy merupakan algoritma yang sederhana dan lempeng (straightforward). Secara harfiah greedy artinya rakus atau tamak.

Algoritma Greedy membentuk solusi langkah per langkah. Terdapat banyak pilihan yang perlu dieksplorasi pada setiap langkah solusi. Oleh karena itu, pada setiap langkah harus dibuat keputusan yang terbaik dalam menentukan pilihan. 

Dalam bahasan ini, fungsi heuristik yang akan kita tampilkan yaitu adalah sebagai berikut.
- h₁(n) : sebagai banyak grid yang menempati tempat yang salah.
- h₂(n) : sebagai total keseluruhan jarak tiap grid yang menempati tempat yang salah terhadap posisi grid yang benar, atau sering disebut dengan manhattan distance.

Solusi Penyelesaian dengan fungsi Heuristik Pertama yaitu banyak grid yang menempati tempat yang salah

![8puzzle-heuristic1.1](https://user-images.githubusercontent.com/52326074/77029102-58f6c180-69cd-11ea-9571-7a69fe89de7d.PNG)
![8puzzle-heuristic1.2](https://user-images.githubusercontent.com/52326074/77029100-585e2b00-69cd-11ea-8d32-03512709f26c.PNG)
![8puzzle-heuristic1.3](https://user-images.githubusercontent.com/52326074/77029097-572cfe00-69cd-11ea-845e-7e8b50514214.PNG)

Solusi :
Initial State -> Right -> Up -> Right -> Down -> Down -> Left -> Up -> Right -> Down(Goal)

Solusi Penyelesai dengan fungsi Heuristik Kedua yaitu total keseluruhan jarak tiap grid yang menempati tempat yang salah terhadap posisi grid yang benar, atau sering disebut dengan manhattan distance.

![8puzzle-heuristic2.1](https://user-images.githubusercontent.com/52326074/77029181-8f344100-69cd-11ea-9799-24cda528fdd5.PNG)
![8puzzle-heuristic2.2](https://user-images.githubusercontent.com/52326074/77029178-8e9baa80-69cd-11ea-9d35-2282c1916e48.PNG)
![8puzzle-heuristic2.3](https://user-images.githubusercontent.com/52326074/77029175-8d6a7d80-69cd-11ea-8775-2fd302b4ad62.PNG)

Solusi :
Initial State -> Right -> Up -> Right -> Down -> Down -> Left -> Up -> Right -> Up(Goal)


Kesimpulannya, dari semua yang telah dipaparkan diatas, penggunaan dari dua fungsi heuristik Algoritma Greedy pada solusi penyelesaian 8-puzzle, baik fungsi heuristik pertama dan kedua sama sama mampu memberikan solusi penyelesaian dari awal state sampai ke goal state. Tetapi menurut pendapat saya, pada penggunaan fungsi heuristik pertama jumlah State puzzle yang memiliki fungsi heuristik yang sama lebih banyak dari pada penggunaan fungsi heuristik kedua. Jadi, penggunaan solusi dari fungsi heuristik kedua dalam contoh penyelesaian 8-puzzle diatas lebih optimal dari pada fungsi heuristik pertama.

# 6. 8 Queen Hill Climbing

Dalam program, bagian untuk mengecek apakah sebuah queen bisa diserang oleh queen lain bisa dilihat pada program dibawah ini.
```
int is_attack(int i,int j) {
    int k,l;
    //checking if there is a queen in row or column
    for(k=0;k<N;k++) {
        if((board[i][k] == 1) || (board[k][j] == 1))
            return 1;
    }
    //checking for diagonals
    for(k=0;k<N;k++) {
        for(l=0;l<N;l++) {
            if(((k+l) == (i+j)) || ((k-l) == (i-j))) {
                if(board[k][l] == 1)
                    return 1;
            }
        }
    }
    return 0;
}
```

Kemudian, setelah dirasa tidak ada queen yang menyerang, maka program dibawah ini merupakan bagian untuk meletakkan queen yang dirasa aman.
```
int N_queen(int n) {
    int i,j;
    //if n is 0, solution found
    if(n==0)
        return 1;
    for(i=0;i<N;i++) {
        for(j=0;j<N;j++) {
            //checking if we can place a queen here or not
            //queen will not be placed if the place is being attacked
            //or already occupied
            if((!is_attack(i,j)) && (board[i][j]!=1)) {
                board[i][j] = 1;
                //recursion wether we can put the next queen with this arrangment or not
                if(N_queen(n-1)==1) {
                    return 1;
                }
                board[i][j] = 0;
            }
        }
    }
    return 0;
}
```

Hill Climbing adalah pencarian heuristik yang digunakan untuk masalah optimasi matematis di bidang Inteligensi Buatan.

Dengan sejumlah besar input dan fungsi heuristik yang baik, ia mencoba untuk menemukan solusi yang cukup baik untuk masalah tersebut. Solusi ini mungkin bukan global optimal maksimum.
- Dalam definisi di atas, `Mathematical Optimization Problems` menyiratkan bahwa mendaki bukit memecahkan masalah di mana kita perlu memaksimalkan atau meminimalkan fungsi nyata yang diberikan dengan memilih nilai dari input yang diberikan. Contoh-Traveling salesman masalah di mana kita perlu meminimalkan jarak yang ditempuh oleh salesman.
- `Heuristic Search` berarti bahwa algoritma pencarian ini mungkin tidak menemukan solusi optimal untuk masalah tersebut. Namun, itu akan memberikan solusi yang baik dalam waktu yang wajar.
- `Heuristic Function` adalah fungsi yang akan memberi peringkat semua alternatif yang mungkin pada setiap langkah percabangan dalam algoritma pencarian berdasarkan informasi yang tersedia. Ini membantu algoritma untuk memilih rute terbaik dari rute yang mungkin.

![hc](https://user-images.githubusercontent.com/52326074/77150635-e36f1c00-6ac6-11ea-977e-153dd3b862e3.png)

## Fitur Hill Climbing
### a. Varian dari menghasilkan dan menguji algoritma

Ini adalah varian dari algoritma generate and test. Algoritma generate and test adalah sebagai berikut:
- Hasilkan solusi yang mungkin.
- Tes untuk melihat apakah ini solusi yang diharapkan.
- Jika solusinya telah ditemukan, keluar lagi, lanjutkan ke langkah 1.

Oleh karena itu kami menyebut Hill climbing sebagai varian dari algoritma hasil dan uji karena mengambil umpan balik dari prosedur pengujian. Kemudian umpan balik ini digunakan oleh generator dalam memutuskan langkah selanjutnya dalam ruang pencarian.

### b. Menggunakan Greedy Aproach

Pada titik mana pun di ruang keadaan, pencarian bergerak ke arah itu saja yang mengoptimalkan biaya fungsi dengan harapan menemukan solusi optimal di akhir.

## Jenis Hill Climbing
### a. Steepest-Ascent Hill Climbing

Pertama-tama memeriksa semua node tetangga dan kemudian memilih simpul yang paling dekat dengan keadaan solusi pada simpul berikutnya.

- Evaluasi keadaan awal. Jika status tujuan maka keluar dari yang lain jadikan status saat ini sebagai keadaan awal
- Ulangi langkah ini sampai solusi ditemukan atau keadaan saat ini tidak berubah
- Exit

### b. Simple Hill Climbing

Ini memeriksa node tetangga satu per satu dan memilih node tetangga pertama yang mengoptimalkan biaya saat ini sebagai node berikutnya. Ini memeriksa node tetangga satu per satu dan memilih node tetangga pertama yang mengoptimalkan biaya saat ini sebagai node berikutnya.

Algoritma Simple Hill climbing :
- Evaluasi keadaan awal. Jika itu adalah keadaan tujuan maka berhentilah dan kembalikan kesuksesan. Kalau tidak, jadikan kondisi awal sebagai kondisi saat ini.
- Loop sampai keadaan solusi ditemukan atau tidak ada operator baru yang dapat diterapkan ke keadaan saat ini.
- Exit

### c. Stochastic Hill Climbing

Itu tidak memeriksa semua node tetangga sebelum memutuskan node mana yang akan dipilih. Itu hanya memilih node tetangga secara acak dan memutuskan (berdasarkan jumlah peningkatan tetangga itu) apakah akan pindah ke tetangga itu atau untuk memeriksa yang lain.

# 7. Minimax - Tic Tac Toe

Dalam permasalahan minimax, selain menentukan nilai min maupun max dalam sekelompok angka, namun juga bisa diaplikasikan dalam penyelesaian tic tac toe game. Pastinya dalam menjalankan permainan ini, dilakukan secara bergiliran untuk meletakkan karakter pada kolom yang disediakan.

Pada bagian dibawah ini untuk mendeteksi pada kolom apakah sudah terisi karakter `X` atau `O` atau bahkan kosong ` `.
```c
char gridChar(int i) {
    switch(i) {
        case -1:
            return 'X';
        case 0:
            return ' ';
        case 1:
            return 'O';
    }
}
```

Untuk bagian dibawah ini, mencetak board tic tac toe.
```c
void draw(int b[9]) {
    printf(" %c | %c | %c\n",gridChar(b[0]),gridChar(b[1]),gridChar(b[2]));
    printf("---+---+---\n");
    printf(" %c | %c | %c\n",gridChar(b[3]),gridChar(b[4]),gridChar(b[5]));
    printf("---+---+---\n");
    printf(" %c | %c | %c\n",gridChar(b[6]),gridChar(b[7]),gridChar(b[8]));
}
```

Kemudian, fungsi program dibawah ini untuk mengecek setelah player melakukan langkah / mengisi karakter pada board itu mencapai kemenangan (sudah terbentuk garis).
```c
int win(const int board[9]) {
    //determines if a player has won, returns 0 otherwise.
    unsigned wins[8][3] = {{0,1,2},{3,4,5},{6,7,8},{0,3,6},{1,4,7},{2,5,8},{0,4,8},{2,4,6}};
    int i;
    for(i = 0; i < 8; ++i) {
        if(board[wins[i][0]] != 0 &&
           board[wins[i][0]] == board[wins[i][1]] &&
           board[wins[i][0]] == board[wins[i][2]])
            return board[wins[i][2]];
    }
    return 0;
}
```

Sedangkan untuk bagian dibawah ini, untuk berjalannya tic tac toe dengan mengecek perpindahan player meletakkan karakter pada board dengan menggunakan metode minimax.
```c
int minimax(int board[9], int player) {
    //How is the position like for player (their turn) on board?
    int winner = win(board);
    if(winner != 0) return winner*player;

    int move = -1;
    int score = -2;//Losing moves are preferred to no move
    int i;
    for(i = 0; i < 9; ++i) {//For all moves,
        if(board[i] == 0) {//If legal,
            board[i] = player;//Try the move
            int thisScore = -minimax(board, player*-1);
            if(thisScore > score) {
                score = thisScore;
                move = i;
            }//Pick the one that's worst for the opponent
            board[i] = 0;//Reset board after try
        }
    }
    if(move == -1) return 0;
    return score;
}
```

Bagian dibawah ini untuk lawan / dalam hal ini dibuat computer sebagai lawan untuk berjalan menentukan letak karakter.
```c
void computerMove(int board[9]) {
    int move = -1;
    int score = -2;
    int i;
    for(i = 0; i < 9; ++i) {
        if(board[i] == 0) {
            board[i] = 1;
            int tempScore = -minimax(board, -1);
            board[i] = 0;
            if(tempScore > score) {
                score = tempScore;
                move = i;
            }
        }
    }
    //returns a score based on minimax tree at a given node.
    board[move] = 1;
}
```

Sedangkan bagian dibawah ini untuk player utama berjalan menentukan letak karakter.
```c
void playerMove(int board[9]) {
    int move = 0;
    do {
        printf("\nInput move ([0..8]): ");
        scanf("%d", &move);
        printf("\n");
    } while (move >= 9 || move < 0 && board[move] == 0);
    board[move] = -1;
}
```

Tic Tac Toe merupakan permainan yang dimainkan oleh 2 pemain dengan menempatkan ‘buah’ yang berlainan untuk tiap pemain pada kotak 3 x 3. Penempatan ‘buah’ dilakukan secara bergantian sehingga salah satu pemain menjadi pemenang atau seluruh kotak terisi oleh ‘buah’. Salah satu pemain dikatakan menang jika dapat menempatkan ‘buah’ berjajar sebanyak 3 buah baik secara horisontal, vertikal atau diagonal.

Dalam permainan ini kita harus berusaha untuk memaksimalkan kemungkinan untuk mencapai kemenangan pemain pertama dan meminimalkan kemungkinan kemenangan lawan (pemain kedua).

Komponen penelusuran dalam aplikasi minimax pada permainan Tic Tac Toe ini adalah :

- `Initial state` merupakan keadaan saat pencarian akan dilakukan, pada saat permainan mulai dilakukan (jika pemain pertama jalan pertama), initial statenya adalah :

![tictactoe.1](https://user-images.githubusercontent.com/52326074/77034748-4dab9200-69dd-11ea-8215-48c660f28237.JPG)

Initial state selalu berubah saat giliran jalan pemain pertama.
- `Operator (rule/ilegal moves)`, Operator pada permainan ini adalah pemain dapat meletakkan ‘buah’ nya secara sembarang di kotak yang masih kosong.
- `Terminal Test` adalah keadaan dimana komposisi terbaik yang dilakukan pemain pertama setelah diadakan penelusuran.
- `Utility function` pada permainan ini adalah mencari kemungkinan kemenangan bagi pemain pertama dikurangi dengan kemungkinan kemenangan dari pemain lawan. Pada saat permainan dimulai masing-masing kemungkinan kemenangan tiap pemain adalah 8 yaitu 3 horisontal + 3 vertikal + 2 diagonal.

![tictactoe.2](https://user-images.githubusercontent.com/52326074/77034890-b561dd00-69dd-11ea-9a93-b8adca75b3e8.JPG)

Contoh pada komposisi :

![tictactoe.3](https://user-images.githubusercontent.com/52326074/77034911-c4488f80-69dd-11ea-904e-87b6294917db.JPG)

Kemungkinan kemenangan pemain pertama adalah 6, sedangkan kemungkinan kemenangan pemain kedua adalah 5.

![tictactoe.4](https://user-images.githubusercontent.com/52326074/77034938-d88c8c80-69dd-11ea-845c-596e936eaad9.JPG)

Jadi nilai untuk komposisi di atas adalah 6 – 5 = 1.

Dari keadaan permainan dimulai, graph minimax untuk Two-Ply Search dapat digambarkan sebagai berikut (X = pemain pertama, O = pemain kedua):

![tictactoe.5](https://user-images.githubusercontent.com/52326074/77034975-efcb7a00-69dd-11ea-97ae-2ff5b0943d04.JPG)

Nilai node E sampai P didapat dari utility function yang telah didefinisikan sebelumnya sehingga didapatkan :
```
E = 6 – 5 = 1
F = 5 – 5 = 0
G = 6 – 5 = 1
H = 5 – 5 = 0
I = 4 – 5 = -1
J = 5 – 4 = 1
K = 6 – 4 = 2
L = 5 – 6 = -1
M = 5 – 5 = 0
N = 5 – 6 = -1
O = 6 – 6 = 0
P = 4 – 6 = -2
```

Ada sembilan langkah yang mungkin dilakukan oleh pemain pertama karena kotak kosongnya berjumlah 9, tapi pada diagram diatas hanya diambil 3 kemungkinan (node B,C dan D), karena 6 kemungkinan lainnya setara dengan ke-3 komposisi di atas, misalnya :

![tictactoe.6](https://user-images.githubusercontent.com/52326074/77035007-083b9480-69de-11ea-9932-0b194195291b.JPG)

Dari node B seharusnya didapatkan node anak sebanyak 8 node, dengan mengabaikan node yang setara node anak dari B menjadi E, F, G, H dan I. Dengan cara yang sama didapatkan node anak dari C yaitu J dan K, sedangkan node anak dari D yaitu L, M, N, O dan P.

Karena hanya menggunakan Two-Ply Search, node-node anak dari B, C dan D dicari nilainya, kemudian dicari yang terkecil (min) masing-masing untuk dijadikan nilai B, C dan D. Selanjutnya dicari nilai terbesar (max) dari ketiga nilai tersebut untuk menentukan langkah pemain pertama.

Pada diagram yang digambarkan diatas, node anak dari B bernilai masing-masing E=1, F=0, G=1, H=0 dan I=-1 jadi nilai B diambil yang terkecil yaitu –1.

Node anak dari C bernilai masing-masing J=1 dan K=2 jadi nilai C diambil yang terkecil yaitu 1. Kemudian node anak dari D bernilai masing-masing L=-1, M=0, N=-1, O=0 dan P=-2 jadi nilai C diambil yang terkecil yaitu –2.

Selanjutnya dari nilai node B=-1, C=1, dan D=-2 diambil nilai terbesar yaitu C=1, yang berarti langkah terbaik yang harus dilakukan oleh pemain pertama adalah node C.

Setelah pemain kedua menempatkan buahnya, keadaan saat itu dijadikan initial state dan dilakukan kembali pelacakan dengan langkah yang telah dijelaskan di atas. Contoh : Misalkan pemain kedua meletakkan buahnya seperti gambar berikut :

![tictactoe.7](https://user-images.githubusercontent.com/52326074/77035046-21444580-69de-11ea-89a1-5eeb2dd345c4.JPG)

Dari keadaan ini, graph minimax untuk Two-Ply Search dapat digambarkan sebagai berikut (X = pemain pertama, O = pemain kedua):

![tictactoe.8](https://user-images.githubusercontent.com/52326074/77035066-2e613480-69de-11ea-816d-f67b069d2523.JPG)

Dari diagram diatas, langkah terbaik yang dapat dilakukan oleh pemain pertama terdapat dua pilihan yaitu B(1) dan D(1).


# 9. 4 Queen
Pada problem N queen ini digunakan algoritma backtracking, yaitu mencoba menaruh queen dimulai dari kolom atas kiri atau kolom pertama baris pertama, lalu kita mencoba menaruh queen lain dan di cek apakah ada yang saling melawan atau tidak. Jika saat kita menaruh queen dan tidak ada yang saling melawan dengan queen lain maka baris dan kolomnya akan dijadikan sebagai bagian dari solusi, bila pada hasil akhir tidak ditemukan hasil yang tepat karena masih ada queen yang saling melawan, maka akan di backtrack dan return false.

Fungsi untuk menaruh queen
```c
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
```



