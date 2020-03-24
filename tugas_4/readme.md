# KECERDASAN BUATAN - F

Brananda Denta Wira Pranata - 05111840000030

Teknik Informatika - Fakultas Teknologi Elektro & Informatika Cerdas

Institut Teknologi Sepuluh Nopember Surabaya

# 4 Queen

define N 4 karena ingin 4 queen

Membuat fungsi untuk bisa mewarnai karakter
```
void Color(int col) {  
HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);  
SetConsoleTextAttribute(hConsole, col);  
}  
```
lalu setelah itu, kita harus membuat fungsi untuk memberitahu bahwa apakah aman jika queen diletakkan di tempat tersebut, fungsi akan return true jika aman, dan akan return false jika tidak aman
```
bool isSafe(int board[N][N], int row, int col) {  
int i, j;  

for (i = 0; i < col; i++)  
    if (board[row][i]) return false;  

for (i = row, j = col; i >= 0 && j >= 0; i--, j--)  
    if (board[i][j]) return false;  

for (i = row, j = col; j >= 0 && i < N; i++, j--)  
    if (board[i][j]) return false;  
return true;  
}  
```

```
for (i = 0; i < col; i++)  
    if (board[row][i]) return false;  
```
for di atas digunakan untuk cek baris di sisi kiri

```
for (i = row, j = col; i >= 0 && j >= 0; i--, j--)  
    if (board[i][j]) return false; 
```
for di atas untuk memeriksa diagonal atas di sisi kiri 

```
for (i = row, j = col; j >= 0 && i < N; i++, j--)  
    if (board[i][j]) return false; 
```
for diatas digunakan untuk memeriksa diagonal bawah di sisi kiri

lalu buat fungsi untuk dapat memindahkan ratu secara aman
```
bool solveNQUtil(int board[N][N], int col) {  
/* base case: Jika semua ratu ditempatkan lalu return true */  
if (col >= N) return true;  
/* Pertimbangkan kolom  dan coba tempatkan ratu di semua baris satu per satu */  
for (int i = 0; i < N; i++) {  
    /* Periksa apakah ratu dapat ditempatkan pada board[i][col] */  
    if (isSafe(board, i, col)) {  
        /* Tempatkan ratu pada board[i][col] */  
        board[i][col] = 1;  
        /* berulang untuk menempatkan sisa ratu */  
        if (solveNQUtil(board, col + 1)) return true;  
        /* Jika menempatkan ratu di board[i][col] 
        tidak mengarah ke solusi, lalu hapus ratu dari board[i][col] */  
        board[i][col] = 0; // BACKTRACK  
    }  
}  
/* Jika ratu tidak dapat ditempatkan di baris mana pun di kolom col ini, lalu
 return false */  
return false;  
}  
```

lalu membuat fungsi untuk membuat board
```
bool solveNQ() {  
    int board[N][N] = {  
        {  
            0,  
            0,  
            0,  
            0  
        },  
        {  
            0,  
            0,  
            0,  
            0  
        },  
        {  
            0,  
            0,  
            0,  
            0  
        },  
        {  
            0,  
            0,  
            0,  
            0  
        }  
    };  
    if (solveNQUtil(board, 0) == false) {  
        printf("Solution does not exist");  
        return false;  
    }  
        printSolution(board);  
        return true;  
}  



