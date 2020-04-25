* Gambar hasil compile & run https://github.com/dentaaa/KB_F_05111840000143/blob/master/tugas2/image.png

         #include<cstdlib>
         #include<iostream>
         using namespace std;

        int pawn[8][8];
        int board[8][8];

        //Untuk mencari nilai maksnya
          int match(){
	        int k, l, m, n=0;
            for(k=0; k<8; k++) {
               for(l=0; l<8; l++) {
                if(board[k][l] == 1) {
                  for(m=1; m<8; m++) {
                    if(k+m < 8) {
                        if(l+m < 8) {
                            if(board[k+m][l+m] == 1) {
                            	n++;	
							          }
                }
                        if(l-m > -1) {
                            if(board[k+m][l-m] == 1) {
                            	n++;	
							}
                        }
                    }
                    if(k-m > -1) {
                        if(l+m < 8) {
                            if(board[k-m][l+m] == 1) {
                            	n++;	
							}
                        }
                        if(l-m > -1) {
                            if(board[l-m][l-m] == 1) {
                            	n++;	
							}
                        	}
                    	 }                      
               	     }
                 }
             }
          }
    	   return n;
	  }

	  //Untuk mencari nilai maks di setiap koordinat x dan y
	  int xy (int x, int y){
          int k, l, m, n=0;
    		for(k=1; k<8; k++){
      		  if(x+k < 8){
            	  if(y+k < 8){
                  if(board[x+k][y+k] == 1){
                  n++;	
		}
            }
            if(y-k > -1){
                if(board[x+k][y-k] == 1){
                	n++;	
		}
            }
        }
        if(x-k > -1){
            if(y+k < 8){
                if(board[x-k][y+k] == 1){
                	n++;	
		}
            }
            if(y-k > -1){
                if(board[x-k][y-k] == 1){
                	n++;	
		 }
             }
         }
      }
      return n;
      }

	  //Fungsi untuk membandingkan nilai maks memakai metode hill climbing
	  void hillclimb (int t) {
   	  int h1 = t, x1, y1, htmp, div, temp, i, j, k;
   	  if (t == 0) {
       		for(i=0; i < 8; i++){
           	cout <<"("<<pawn[i][0]+1<<","<<pawn[i][1]+1<<")"<< endl;
        }
        return;
        }
    	for(i=0; i<8; i++) {
        	temp = xy (pawn[i][0], pawn[i][1]);
        	temp = t - temp;
        	board [pawn[i][0]] [pawn[i][1]] = 0;
        for(j=0; j<8; j++) {
            for(k=0; k<8; k++) {
                if(board[j][k] == 0) {
                    htmp = xy (j,k);
                    if(htmp + temp < h1) {
                        h1 = htmp + temp;
                        x1 = j;
                        y1 = k;
                        div = i;
                     }
                }
            }
        }
        board [pawn[i][0]] [pawn[i][1]] = 1;
      }
      if(h1 < t) {
         board [pawn[div][0]] [pawn[div][1]] = 0;
         pawn [div][0] = x1;
         pawn [div][1] = y1;
    	 board [pawn[div][0]] [pawn[div][1]] = 1;
         hillclimb (h1);
      }
          else {
        	return;}
	  }

	  int main() {
          int i=0, a, b;
    	  while (i < 8) {
       		 a = rand() % 8;
      	         b = rand() % 8;
          if(board[a][b] == 0) {
            board[a][b] = 1;
            pawn[i][0] = a;
            pawn[i][1] = b;
            i++;
       		 }
   	    }
   	  for(i=0; i<8; i++) {
       		 cout <<"("<<pawn[i][0]<<","<<pawn[i][1]<<")";
    	  }
    	   hillclimb (match());
	  }
