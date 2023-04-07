# 🐈 requests > *;

```cs
using Newtonsoft.Json;
using System.Collections.Generic;
using System.Threading;
using System.Net;
using System.Threading.Tasks;
using System.Net.Http;
using System;

namespace practice
{
    internal class Program
    {
        public static async Task Main(string[] args)
        {
            ServicePointManager.Expect100Continue = false;
            ServicePointManager.DefaultConnectionLimit = 1000;

            var threads = new List<Thread>();

            for(int i =0; i < 12000; i++)
            {
                threads.Add(new Thread(async () =>
                {
                    var client = new HttpClient();

                    HttpResponseMessage response = await client.GetAsync("https://dog.ceo/api/breeds/image/random");
                    string content = await response.Content.ReadAsStringAsync();
                    var json = JsonConvert.DeserializeObject<dynamic>(content);

                    await Console.Out.WriteLineAsync(json["message"].ToString());
                }));
            }

            threads.ForEach(t => t.Start());
            threads.ForEach(t => t.Join());
        }
    }
}

```
