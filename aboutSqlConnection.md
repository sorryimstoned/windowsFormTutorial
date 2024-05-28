# Подключение для чтения с ExecuteReader 

```
string connectionString = ""; //строка подключения
using (SqlConnection connection = new SqlConnection(connectionString))
{
    connection.Open();
    string query = "select * from table";
    var cmd = new SqlCommand(query, connection);
    using (var reader = cmd.ExecuteReader())
    {
        while (reader.Read())
        {
        	object valueObj = reader.GetObject(1); //сразу тип из бд
            string value = reader.GetString(1); 

            if (name == textBox1.Text && password == textBox2.Text)
            {
                exist = true;
                break;
            }
        }
    }
}
```

# Подключение для вставки и удаления с ExecuteNonQuery

```
string connectionString = ""; //строка подключения
using (SqlConnection connection = new SqlConnection(connectionString))
{
    connection.Open();

    string v1 = ""; 
    string id1 = "";

    string queryInsert = $"insert into table values ('{v1}')"; //вставка
	string query = $"delete from table where id = '{id1}'";

    var cmd = new SqlCommand(queryInsert, connection);
    try 
	{
		int numOfRowWichWorked = cmd.ExecuteNonQuery(); //возвращает колличество строк с которыми работал
	}
	catch (Exception ex) //обязательно ex
	{
		Message.Show(ex);
	}
}
``` 
# data grid refresh

```
using (SqlConnection connection = new SqlConnection(connectionString))
{
	SqlCommand cmd = new SqlCommand("select * from table", connection);
	SqlDataAdapter adapter = new SqlDataAdapter();
	DataTable dataTable = new DataTable();

	adapter.Fill(dataTable);

	dataGridView.DataSource = dataTable;
}
```

