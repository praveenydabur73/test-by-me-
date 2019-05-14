 public static List<Dictionary<string, object>> ConvertToDictionary(this SqlDataReader reader)
        {
            try
            {
                List<string> columns = new List<string>();
                List<Dictionary<string, object>> rows = new List<Dictionary<string, object>>();

                for (var i = 0; i < reader.FieldCount; i++)
                {
                    if (!columns.Contains(reader.GetName(i)))
                        columns.Add(reader.GetName(i));
                }

                while (reader.Read())
                {
                    rows.Add(columns.ToDictionary(column => column, column => reader[column]));
                }

                return rows;
            }
            catch (Exception ex)
            {
                throw ex;
            }
        }
