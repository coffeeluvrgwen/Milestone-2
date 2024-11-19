using System;
using System.Collections.Generic;
using System.Linq;
using Newtonsoft.Json;
using System.Net;
using System.IO;

namespace MicroserviceA
{
    internal class MicroserviceA
    {
        public static string SongGroups(List<string> songTitles)
        {
            var alphabeticalGroups = songTitles
                .GroupBy(title => title[0].ToString().ToUpper())
                .ToDictionary(g => $"Starts with '{g.Key}'", g => g.ToList());

            var result = new Dictionary<string, object>
            {
                { "Alphabetical Groups:", alphabeticalGroups },
            };
            return JsonConvert.SerializeObject(result, Formatting.Indented);

        }
        static void Main(string[] args)
        {
            HttpListener listener = new HttpListener();
            listener.Prefixes.Add("http://localhost:8081/");
            listener.Start();
            Console.WriteLine("The program is listenining for data...");

            HttpListenerContext context = listener.GetContext();
            Console.WriteLine("Request received!");
            HttpListenerRequest request = context.Request;

            string json = "";
            string result = "";
            List<string> songTitles = new List<string>();

            try
            {
                using (var reader = new StreamReader(request.InputStream))
                {
                    json = reader.ReadToEnd();
                }

                Console.WriteLine("The program has received JSON data: ");
                Console.WriteLine(json);

                var deserializedTitles = JsonConvert.DeserializeObject<List<string>>(json);
                if (deserializedTitles != null)
                {
                    songTitles = deserializedTitles;
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }

            result = SongGroups(songTitles);

            try
            {
                var response = context.Response;
                response.ContentType = "application/json";
                using (var writer = new StreamWriter(response.OutputStream))
                {
                    writer.Write(result);
                }

                Console.WriteLine("Response sent to client.");
                response.Close();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error sending response: {ex.Message}");
            }
        }
    }
}
