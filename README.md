# ex10_33_my_thinking
自己理解答案的过程

编写程序，接受三个参数：一个输入文件和两个输出文件的文件名。输入文件保存的是整数。使用
istream_iterator读取输入文件。使用ostream_iterator将奇数写入第一个输出文件，每个值之后
都跟一个空格。将偶数写入第二个输出文件，每个值都独占一行。

//  Write a program that takes the names of an input file and two output files.
//  The input file should hold integers. Using an istream_iterator read the
//  input file.
//  Using ostream_iterators, write the odd numbers into the first output file.
//  Each value should be followed by a space.Write the even numbers into the
//  second file.
//  Each of these values should be placed on a separate line.
//
//  Run: ./a.out "../data/input.txt" "../data/odd.txt" "../data/even.txt"

     #include <fstream>
    #include <iterator>
    #include <algorithm>

    int main(int argc, char** argv)
    {
        if (argc != 4) return -1;

        std::ifstream ifs(argv[1]);
        std::ofstream ofs_odd(argv[2]), ofs_even(argv[3]);

        std::istream_iterator<int> in(ifs), in_eof;
        std::ostream_iterator<int> out_odd(ofs_odd, " "), out_even(ofs_even, "\n");

        std::for_each(in, in_eof, [&out_odd, &out_even](const int i) {
            *(i & 0x1 ? out_odd : out_even)++ = i;
            //
            //
        });

        return 0;
    }
    
 从[&out_odd到 =i;结束，这个一个lambda，捕获引用
     *(i & 0x1 ? out_odd : out_even)++ = i;
     这个的意思，其实它解引的是i，因为for_each()，从in到in_eof中的所有元素都要执行后边的lambda（可调用对象）
     而in到in_eof是istream_iterator，i其实是迭代器，所以要解引i
     解引的是该迭代器的保存的副本，迭代器其实已经++，向前移动了
     第一个元素，迭代器i将元素送左边处理，随后迭代器++
     【还是有些不理解，先写到这】
     i如果为奇数，就给odd，否则就给even
     
     
