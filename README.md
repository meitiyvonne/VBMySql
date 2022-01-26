# VBMySql

using MySql.Data.MySqlClient;
using System;
using System.Data;

namespace ConnMySql
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Connect to Database Engine: MySQL5.7!");

            // 1. setup SQL engine
            string connstring = @"server=localhost; userid=root;password=root;database=test";

            // 2. import MySQL library: MySql.Data.MySqlClient
            MySqlConnection conn = null;

            try
            {
                // 3. test connection
                conn = new MySqlConnection(connstring);

                // 4. open sql connection
                conn.Open();

                // 5. setup query language
                string query = "select * from data";

                // 6. instantial an object of MySqlDataAdapter
                MySqlDataAdapter da = new MySqlDataAdapter(query, conn);

                // 7. prepare a container for data
                DataSet ds = new DataSet();

                // 8. fill out the container ds by tb_data
                da.Fill(ds, "data");

                // 9. make dataTable array
                DataTable dt = ds.Tables["data"];

                // 10. iterator data source, read out each row | columns
                foreach(DataRow row in dt.Rows)
                {
                    foreach(DataColumn col in dt.Columns)
                    {
                        Console.Write(row[col] + "\t");
                    }

                    Console.Write("\n");
                }

                Console.ReadKey();
            }
            catch(Exception e)
            {
                Console.WriteLine($"Error: {e} exception caught");
            }
            finally
            {
                // 11. close connection to Data Server Engine
                if (!conn.Equals(null))
                {
                    conn.Close();
                }
            }

        }
    }
}
