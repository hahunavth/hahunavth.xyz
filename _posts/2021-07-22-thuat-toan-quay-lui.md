---
title: Backtracking - Thuật toán quay lui
author: Hahunavth
date: 2121-07-22 06:10:00 +0700
categories: [Algorithm]
tags: [code, C]
---

## Giới thiệu
Backtracking là một thuật toán-kỹ thuật để giải quyết các vấn đề một cách đệ quy bằng cách cố gắng xây dựng một giải pháp từng bước, từng phần một, loại bỏ những giải pháp không thỏa mãn các ràng buộc của vấn đề tại bất kỳ thời điểm nào (theo thời gian, ở đây, được đề cập đến thời gian trôi qua cho đến khi đạt đến bất kỳ cấp độ nào của cây tìm kiếm).

Ví dụ, hãy xem xét Bài toán giải Sudoku, chúng ta thử điền từng chữ số một. Bất cứ khi nào chúng tôi thấy rằng chữ số hiện tại không thể dẫn đến một giải pháp, chúng tôi xóa nó (dấu lùi) và thử chữ số tiếp theo. Cách này tốt hơn cách tiếp cận ngây thơ (tạo ra tất cả các kết hợp có thể có của các chữ số và sau đó thử từng kết hợp một) vì nó giảm một tập hợp các hoán vị bất cứ khi nào nó bị lỗi.

![Sudoku Img](https://sudoku.com/img/post-images/1618508253-Game_Screen_Killer_Mode_%20Color.png)

Theo định nghĩa của wiki,
 > **Backtracking có thể được định nghĩa là một kỹ thuật thuật toán tổng quát xem xét việc tìm kiếm mọi kết hợp có thể có để giải quyết một vấn đề tính toán.**

Có ba loại vấn đề trong backtracking:
1. Vấn đề Quyết định - Trong vấn đề này, chúng tôi tìm kiếm một giải pháp khả thi.
2. Vấn đề tối ưu hóa - Trong vấn đề này, chúng tôi tìm kiếm giải pháp tốt nhất.
3. Bài toán liệt kê - Trong vấn đề này, chúng tôi tìm thấy tất cả các giải pháp khả thi.

## Bài toán con mã (The Knight’s tour problem)

Backtracking là một mô hình thuật toán thử các giải pháp khác nhau cho đến khi tìm ra giải pháp “hoạt động”. Các vấn đề thường được giải quyết bằng kỹ thuật backtracking có đặc điểm chung sau đây. Những vấn đề này chỉ có thể được giải quyết bằng cách thử mọi cấu hình có thể và mỗi cấu hình chỉ được thử một lần. Một giải pháp Naive cho những vấn đề này là thử tất cả các cấu hình và xuất ra một cấu hình tuân theo các ràng buộc vấn đề đã cho. Backtracking hoạt động theo cách gia tăng và là một tối ưu hóa so với giải pháp Naive, nơi tất cả các cấu hình có thể được tạo và thử.

### Bài toán:
Cho một bảng N * N với quân Mã được đặt trên khối đầu tiên của một bảng trống. Di chuyển theo luật cờ vua phải ghé vào mỗi ô đúng một lần. In thứ tự của từng ô mà chúng được truy cập.

**Ví dụ:**

```Example
Input :
N = 8
Output:
0  59  38  33  30  17   8  63
37  34  31  60   9  62  29  16
58   1  36  39  32  27  18   7
35  48  41  26  61  10  15  28
42  57   2  49  40  23   6  19
47  50  45  54  25  20  11  14
56  43  52   3  22  13  24   5
51  46  55  44  53   4  21  12
```

### Giải quyết vấn đề:

#### **Thuật toán ngây thơ:**
 Tạo tất cả các chuyến tham quan lần lượt và kiểm tra xem chuyến tham quan được tạo có thỏa mãn các ràng buộc hay không.


```code
while there are untried tours
{
   generate the next tour
   if this tour covers all squares
   {
      print this path;
   }
}
```
Backtracking hoạt động theo cách gia tăng để tấn công các vấn đề. Thông thường, chúng tôi bắt đầu từ một vectơ giải pháp trống và thêm từng vật phẩm một (Ý nghĩa của vật phẩm thay đổi theo từng vấn đề. Trong bối cảnh của vấn đề về chuyến tham quan của Knight, một vật phẩm là nước đi của Hiệp sĩ). Khi chúng tôi thêm một mục, chúng tôi sẽ kiểm tra xem việc thêm mục hiện tại có vi phạm ràng buộc vấn đề hay không, nếu có thì chúng tôi xóa mục đó và thử các lựa chọn thay thế khác. Nếu không có lựa chọn thay thế nào hoạt động hiệu quả thì chúng tôi chuyển đến giai đoạn trước và xóa mục đã thêm trong giai đoạn trước. Nếu chúng ta đạt đến giai đoạn ban đầu trở lại thì chúng ta nói rằng không có giải pháp nào tồn tại. Nếu việc thêm một mục không vi phạm các ràng buộc thì chúng tôi thêm đệ quy từng mục một. Nếu vectơ giải pháp trở nên hoàn chỉnh thì chúng tôi in lời giải.

#### **Sử dụng thuật toán quay lui:**

```code
If tất cả các ô vuông được truy cập
  in giải pháp
else
  a) Thêm một trong các bước tiếp theo vào vectơ nghiệm và đệ quy
  kiểm tra xem liệu động thái này có dẫn đến giải pháp hay không. (Một Hiệp sĩ có thể tạo ra tối đa
  tám nước đi. Chúng tôi chọn một trong 8 nước đi trong bước này).
  b) Nếu bước đi được chọn ở bước trên không dẫn đến giải pháp
  sau đó xóa di chuyển này khỏi vectơ giải pháp và thử
  các động thái thay thế.
  c) Nếu không có lựa chọn thay thế nào hoạt động thì trả về false (Trả về false
  sẽ xóa mục đã thêm trước đó trong đệ quy và nếu sai thì
  được trả về bởi lệnh gọi đệ quy ban đầu thì "không có giải pháp nào tồn tại")
```

Sau đây là các cách triển khai cho vấn đề về chuyến tham quan của Knight. Nó in một trong những giải pháp khả thi ở dạng ma trận 2D. Về cơ bản, đầu ra là một ma trận 2D 8 * 8 với các số từ 0 đến 63 và những con số này hiển thị các bước do Knight thực hiện.

```c
#include <stdio.h>
#define N 8

int solveKTUtil(int x, int y, int movei, int sol[N][N],
                int xMove[], int yMove[]);

/* A utility function to check if i,j are valid indexes
   for N*N chessboard */
int isSafe(int x, int y, int sol[N][N])
{
    return (x >= 0 && x < N && y >= 0 && y < N
            && sol[x][y] == -1);
}

/* A utility function to print solution matrix sol[N][N] */
void printSolution(int sol[N][N])
{
    for (int x = 0; x < N; x++) {
        for (int y = 0; y < N; y++)
            printf(" %2d ", sol[x][y]);
        printf("\n");
    }
}

/* This function solves the Knight Tour problem using
   Backtracking.  This function mainly uses solveKTUtil()
   to solve the problem. It returns false if no complete
   tour is possible, otherwise return true and prints the
   tour.
   Please note that there may be more than one solutions,
   this function prints one of the feasible solutions.  */
int solveKT()
{
    int sol[N][N];

    /* Initialization of solution matrix */
    for (int x = 0; x < N; x++)
        for (int y = 0; y < N; y++)
            sol[x][y] = -1;

    /* xMove[] and yMove[] define next move of Knight.
       xMove[] is for next value of x coordinate
       yMove[] is for next value of y coordinate */
    int xMove[8] = { 2, 1, -1, -2, -2, -1, 1, 2 };
    int yMove[8] = { 1, 2, 2, 1, -1, -2, -2, -1 };

    // Since the Knight is initially at the first block
    sol[0][0] = 0;

    /* Start from 0,0 and explore all tours using
       solveKTUtil() */
    if (solveKTUtil(0, 0, 1, sol, xMove, yMove) == 0) {
        printf("Solution does not exist");
        return 0;
    }
    else
        printSolution(sol);

    return 1;
}

/* A recursive utility function to solve Knight Tour
   problem */
int solveKTUtil(int x, int y, int movei, int sol[N][N],
                int xMove[N], int yMove[N])
{
    int k, next_x, next_y;
    if (movei == N * N)
        return 1;

    /* Try all next moves from the current coordinate x, y
     */
    for (k = 0; k < 8; k++) {
        next_x = x + xMove[k];
        next_y = y + yMove[k];
        if (isSafe(next_x, next_y, sol)) {
            sol[next_x][next_y] = movei;
            if (solveKTUtil(next_x, next_y, movei + 1, sol,
                            xMove, yMove)
                == 1)
                return 1;
            else
                sol[next_x][next_y] = -1; // backtracking
        }
    }

    return 0;
}

/* Driver Code */
int main()
{

      // Function Call
    solveKT();
    return 0;
}
```

Output:

```code
0  59  38  33  30  17   8  63
37  34  31  60   9  62  29  16
58   1  36  39  32  27  18   7
35  48  41  26  61  10  15  28
42  57   2  49  40  23   6  19
47  50  45  54  25  20  11  14
56  43  52   3  22  13  24   5
51  46  55  44  53   4  21  12
```
