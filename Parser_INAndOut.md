# Parser ์ธ์ค์์

---

<aside>
๐ก **HEADER**

</aside>

---

# ๊ฐ์

---

์์ ์์ ๋ฐ์ดํฐ๋ฅผ ๋นผ๋ ๋ฐฉ๋ฒ๊ณผ ํ์คํธ๋ฅผ ์์์ ๋ฃ๋ ๊ฒ์ ๋ํ ๋ฌธ์

<aside>
โ ๏ธ ์์ฑ์๊ธฐ 2023๋ 03์

</aside>

<aside>
โ ๏ธ Visual Studio 2022, Excel 2013์์ ์งํ๋์์ต๋๋ค.

</aside>

---

## ์ด ์ฝ๋๋ฅผ ์คํํ๊ธฐ ์  Visual Studio 2022์์๋ ํ๋ก์ ํธ->์ฐธ์กฐ ์ถ๊ฐ->COM->๊ฒ์์์ 'Excel' ํ์ดํ ํด์ฃผ๋ฉด Microft Excel 15.0 Object Library๊ฐ ๋์ค๋๋ฐ ์ผ์ชฝ ์์๋ฅผ ํด๋ฆญํ์ฌ ์ถ๊ฐํ๊ณ  ํ์ธ์ ๋๋ฌ์ค์ผ ํฉ๋๋ค.

## ์์ ์์ ๋ฐ์ดํฐ๋ฅผ ํ์คํธํ ์ํค๋ ์ฝ๋

<h1> ์ฝ๋ ๋ด์ฉ </h1>


```C#
 string excelFilePath = @"C:\Users\SESI\Downloads\language.howtoplay.xlsx";
 string textFilePath = @"C:\Users\SESI\Downloads\Excel_practice\ExcelText1.txt";
```
* string excelFilePath์ string textFilePath๋ ๊ฐ๊ฐ ์์ ํ์ผ์ ๊ฒฝ๋ก์ ํ์คํธ ํ์ผ์ ๊ฒฝ๋ก๋ฅผ ๋ํ๋ด๋ ๋ฌธ์์ด ๋ณ์์๋๋ค.
* excelFilePath์๋ @"์์ ํ์ผ ๊ฒฝ๋ก" 
* textFilePath์๋ @"์ ์ฅํ  ํด๋๊ฒฝ๋ก\์๋ก๋ง๋คํ์ผ์ด๋ฆ.txt" ๋ฅผ ์ ํด์ค๋๋ค. 



```C#

            Excel.Application excel = new Excel.Application();
            Excel.Workbook workbook = null;


```
* Excel.Application์ Excel ์ ํ๋ฆฌ์ผ์ด์์ ๋ํ๋ด๋ COM ๊ฐ์ฒด์๋๋ค. Excel.Application() ์์ฑ์๋ฅผ ํธ์ถํ์ฌ ๊ฐ์ฒด๋ฅผ ๋ง๋ญ๋๋ค.
* Excel.Workbook์ Excel ์ํฌ๋ถ์ ๋ํ๋ด๋ COM ๊ฐ์ฒด์๋๋ค.

```C#
            try
            {
                workbook = excel.Workbooks.Open(excelFilePath);
                Excel.Worksheet worksheet = workbook.Worksheets[1];
```
* try ๋ธ๋ก ์์์ excel.Workbooks.Open(excelFilePath)๋ฅผ ํธ์ถํ์ฌ ์์ ํ์ผ์ ์ฐ ํ Excel.Workbook ๊ฐ์ฒด๋ฅผ ํ ๋นํฉ๋๋ค.
* ์ฒซ ๋ฒ์งธ ์ํฌ์ํธ ๊ฐ์ ธ์ต๋๋ค. 


```C#
 using (StreamWriter sw = new StreamWriter(textFilePath))
                {
                    // ๊ฐ ํ์ ํ์ํ์ฌ ์ ๊ฐ์ ์ฝ์ด ํ์คํธ ํ์ผ์ ์ฐ๊ธฐ
                    for (int row = 1; row <= worksheet.UsedRange.Rows.Count; row++)
                    {
                        for (int col = 1; col <= worksheet.UsedRange.Columns.Count; col++)
                        {
                            // ์ ๊ฐ ์ฝ์ด์ค๊ธฐ
                            Excel.Range range = worksheet.Cells[row, col];
                            string cellValue = (range.Value2 == null) ? "" : range.Value2.ToString();

                            // ํ์คํธ ํ์ผ์ ์ฐ๊ธฐ
                            sw.Write(cellValue);

                            // ๋ง์ง๋ง ์์ด ์๋๋ฉด ๊ตฌ๋ถ์(์ธ๋ฏธ์ฝ๋ก ) ์ฐ๊ธฐ
                            if (col != worksheet.UsedRange.Columns.Count)
                            {
                                sw.Write(";");
                            }
                        }
                        sw.WriteLine(); // ๋ค์ ํ์ผ๋ก ์ด๋ํ์ฌ ์ฐ๊ธฐ
                    }
                }
```


* ์ธํ์ ์๋ฃํ ํ์ ์คํํ๋ฉด ๋ช ์ด์ ์๊ฐ์ด ์ง๋ ํ ํ์คํธ ํ์ผ์ด ์์ฑ๋์๋ค๋ ๋ง๊ณผ ํจ๊ป 

<img src="image/Parser3.PNG" width="100%"><br>

* ์ ํด์ค ํด๋ ์์ ํ์ผ์ด ์๊ธฐ๊ฒ ๋ฉ๋๋ค.

<img src="image/Parser4.PNG" width="100%"><br>

* ๊ทธ ํ์ผ์ ์ด์ด๋ณด๋ฉด ์์ ์์ ๋ฐ์ดํฐ๊ฐ ์ ๋ถ ๋ค์ด๊ฐ ์๊ณ , ์์ด ๊ตฌ๋ถ๋๋ ๋ถ๋ถ์ ';'(์ธ๋ฏธ์ฝ๋ก )์ผ๋ก ์ฐ์ฌ์ก๋ค๋ ๊ฒ์ ์ ์ ์๋๋ฐ.

* ์ด ๋ถ๋ถ์์ sw.Write(";"); ๊ฐ ์์ด ๊ตฌ๋ถ๋๋ ๋ถ๋ถ์ ์ธ๋ฏธ์ฝ๋ก ์ผ๋ก ์ ํ ์ฝ๋์ด๊ณ , ๊ดํธ ์์ ๋ฐ๊พธ์ด์ฃผ๋ฉด ๊ทธ์ ๋ฐ๋ผ ๊ตฌ๋ถ์๋ ๋ฐ๋๊ฒ ๋ฉ๋๋ค.


<์ ์ฒด์ฝ๋>
```C#
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

using System.Runtime.InteropServices;
using System.Data.OleDb;
using System.IO;
using Excel = Microsoft.Office.Interop.Excel;
using Microsoft.Office.Interop.Excel;
using System.Drawing;

namespace Excel_MakeText
{
    internal class Program
    {
        static void Main(string[] args)
        {
            string excelFilePath = @"C:\Users\SESI\Downloads\language.howtoplay.xlsx"; //ํ์คํธ๋ก ๋ง๋ค์ด๋ผ ์์ ํ์ผ์ ๊ฒฝ๋ก ์ง์ 
            string textFilePath = @"C:\Users\SESI\Downloads\Excel_practice\ExcelText1.txt"; //์์ฑํ  ํ์คํธ ํ์ผ์ ์ด๋ฆ๊ณผ ๊ฒฝ๋ก ์ค์  

            Excel.Application excel = new Excel.Application();
            Excel.Workbook workbook = null;

            try
            {
                workbook = excel.Workbooks.Open(excelFilePath);

                // ์ฒซ ๋ฒ์งธ ์ํฌ์ํธ ๊ฐ์ ธ์ค๊ธฐ
                Excel.Worksheet worksheet = workbook.Worksheets[1];

                // ํ์คํธ ํ์ผ ์์ฑ
                using (StreamWriter sw = new StreamWriter(textFilePath))
                {
                    // ๊ฐ ํ์ ํ์ํ์ฌ ์ ๊ฐ์ ์ฝ์ด ํ์คํธ ํ์ผ์ ์ฐ๊ธฐ
                    for (int row = 1; row <= worksheet.UsedRange.Rows.Count; row++)
                    {
                        for (int col = 1; col <= worksheet.UsedRange.Columns.Count; col++)
                        {
                            // ์ ๊ฐ ์ฝ์ด์ค๊ธฐ
                            Excel.Range range = worksheet.Cells[row, col];
                            string cellValue = (range.Value2 == null) ? "" : range.Value2.ToString();

                            // ํ์คํธ ํ์ผ์ ์ฐ๊ธฐ
                            sw.Write(cellValue);

                            // ๋ง์ง๋ง ์์ด ์๋๋ฉด ๊ตฌ๋ถ์(์ธ๋ฏธ์ฝ๋ก ) ์ฐ๊ธฐ
                            if (col != worksheet.UsedRange.Columns.Count)
                            {
                                sw.Write(";");
                            }
                        }
                        sw.WriteLine(); // ๋ค์ ํ์ผ๋ก ์ด๋ํ์ฌ ์ฐ๊ธฐ
                    }
                }

                Console.WriteLine("ํ์คํธ ํ์ผ์ด ์์ฑ๋์์ต๋๋ค.");
            }
            catch (Exception ex)
            {
                Console.WriteLine("์ค๋ฅ๊ฐ ๋ฐ์ํ์์ต๋๋ค: " + ex.Message);
            }
            finally
            {
                if (workbook != null)
                {
                    workbook.Close();
                }
                excel.Quit();

                // COM ์ค๋ธ์ ํธ ํด์ 
                System.Runtime.InteropServices.Marshal.ReleaseComObject(excel);
            }
        }
    }
}


```


---

## ํ์คํธ์์ ์๋ ๋ฐ์ดํฐ๋ฅผ ์์๋ก ์ฎ๊ธฐ๋ ์ฝ๋

ํ์คํธ์ ๋ฐ์ดํฐ๋ค์ ์์ ๋ก ๋ณํ์ํค๋ ์ฝ๋
ํ์คํธ ์์ ์์ ๋จ์๋ฅผ ';'์ง์ ํ์ฌ ๋๋์ด์ค๋๋ค.
* ๋จผ์  ํ์คํธ๋ก ๋ฝ์๋ผ ํ์ผ์ ์์น๋ฅผ ์ง์ ํด์ฃผ์ธ์.
* File.ReadAllLines ํจ์ ์์ ์์น๋ฅผ ์ง์ ํ๋ ๊ณณ์ ๋ฃ์ผ๋ฉด ๋ฉ๋๋ค.


```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

using System.Runtime.InteropServices;
using System.Data.OleDb;
using System.IO;
using Excel = Microsoft.Office.Interop.Excel;
using Microsoft.Office.Interop.Excel;
using System.Drawing;


namespace Excel_makeByText
{
    internal class Program
    {
        static void Main(string[] args)
        {
            
            Application excel = new Application();
            Workbook workbook = excel.Workbooks.Add();
            Worksheet worksheet = workbook.Sheets[1];
            string[] lines = File.ReadAllLines(@"C:\Users\SESI\Downloads\Excel_practice\ExcelText1.txt");

            int row = 1;
            foreach (string line in lines)
            {
                string[] values = line.Split(';');
                int column = 1;
                foreach (string value in values)
                {
                    worksheet.Cells[row, column] = value;
                    worksheet.Columns[column].AutoFit(); // ๊ธ์์ ๊ธธ์ด์ ๋ฐ๋ผ ์์ด ๋์ด๋๋ ์ฝ๋
                    worksheet.Cells[row, column].WrapText = true; //์ธ์ด ์ค๋ฐ๊ฟ์ด ๋๋ ์ฝ๋
                    column++;
                }
                row++;
            }

            string savePath = @"C:\Users\SESI\Downloads\Excel_practice\output.xlsx";
            workbook.SaveAs(savePath);
            workbook.Close();
            excel.Quit();

            //clean up
            ReleaseExcelObject(worksheet);
            ReleaseExcelObject(workbook);
            ReleaseExcelObject(excel);
        }
        private static void ReleaseExcelObject(object obj)
        {
            try
            {
                if (obj != null)
                {
                    Marshal.ReleaseComObject(obj);
                    obj = null;
                }
            }
            catch (Exception ex)
            {
                obj = null;
                throw ex;
            }
            finally
            {
                GC.Collect();
            }
        }
    }
}

```
