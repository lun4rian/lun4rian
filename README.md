# 🐈 requests > *;

```cs
using Newtonsoft.Json;
using System.Collections.Generic;
using System.Threading;
using System.Net;
using System.Threading.Tasks;
using System.Net.Http;
using System;
using System.Text;

namespace practice
{
    internal class Program
    {
        public static async Task Main(string[] args)
        {
            ServicePointManager.Expect100Continue = false;
            ServicePointManager.DefaultConnectionLimit = 1000;

            var threads = new List<Thread>();

            for(int i = 0; i < 1000; i++)
            {
                threads.Add(new Thread(async () =>
                {
                    var client = new HttpClient();

                    var json = new {
                        content = "@everyone @here lunarian is just better"
                    };

                    var json_serialized = JsonConvert.SerializeObject(json);
                    var new_json = new StringContent(json_serialized, Encoding.UTF8, "application/json");

                    client.DefaultRequestHeaders.Add("Authorization", "auth discord token");
                    HttpResponseMessage response = await client.PostAsync("channel message api link", new_json);
                }));
            }

            threads.ForEach(t => t.Start());
            threads.ForEach(t => t.Join());
        }
    }
}
```
