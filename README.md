# Api-Ref
```C#

// using statements for web API libraries
using System;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text;
using System.Threading.Tasks;

namespace WebAPIClient
{
    class Program
    {
        // create a static HttpClient instance to handle requests and responses
        private static readonly HttpClient client = new HttpClient();
      

        static async Task Main(string[] args)
        {
            // set the base address of the web API
            client.BaseAddress = new Uri("https://api.example.com");
            // set the default headers for the client
            client.DefaultRequestHeaders.Accept.Clear();
            client.DefaultRequestHeaders.Accept.Add(
                new MediaTypeWithQualityHeaderValue("application/json"));
            // call a method to use the web API
            await UseWebAPIAsync();
        }

        // define a method to use the web API asynchronously
        private static async Task UseWebAPIAsync()
        {
            try
            {
                // call different methods for different HTTP requests and display the results on console

                // GET request with no parameters
                Console.WriteLine("GET request with no parameters:");
                await GetAsync("endpoint");

                // GET request with headers and authorization parameters
                Console.WriteLine("GET request with headers and authorization parameters:");
                var headers = new Dictionary<string, string>();
                headers.Add("User-Agent", "WebAPIClient");
                var auth = new AuthenticationHeaderValue("Basic", "dXNlcjpwYXNz");
                await GetAsync("endpoint", headers, auth);

                // POST request with content parameter
                Console.WriteLine("POST request with content parameter:");
                var content = new StringContent("{\"name\":\"John\",\"age\":25}", Encoding.UTF8, "application/json");
                await PostAsync("endpoint", content);

                // PUT request with content and authorization parameters
                Console.WriteLine("PUT request with content and authorization parameters:");
                var content2 = new StringContent("{\"name\":\"Jane\",\"age\":30}", Encoding.UTF8, "application/json");
                var auth2 = new AuthenticationHeaderValue("Bearer", "token");
                await PutAsync("endpoint/1", content2,null, auth2);

                // DELETE request with no parameters
                Console.WriteLine("DELETE request with no parameters:");
                await DeleteAsync("endpoint/1");
              
             
                
            }
            catch (HttpRequestException e)
            {
                 // handle any exceptions that occur during the request or response
                 Console.WriteLine("\nException Caught!");
                 Console.WriteLine("Message :{0} ", e.Message);
             }
         }

         // define a generic method to send a GET request asynchronously and return the response as a string 
         private static async Task<string> GetAsync(string endpoint, Dictionary<string, string> headers = null, AuthenticationHeaderValue auth = null)
         {
             // add any custom headers to the client if provided 
             if (headers != null)
             {
                 foreach (var header in headers)
                 {
                     client.DefaultRequestHeaders.Add(header.Key, header.Value);
                 }
             }
             // add any authentication header to the client if provided 
             if (auth != null)
             {
                 client.DefaultRequestHeaders.Authorization = auth;
             }
             // send a GET request to the endpoint and get the response 
             HttpResponseMessage response = await client.GetAsync(endpoint);
             response.EnsureSuccessStatusCode();

             // read the response content as a string and return it 
             string responseBody = await response.Content.ReadAsStringAsync();
             return responseBody;
         }

         // define a generic method to send a POST request asynchronously and return the response as a string 
         private static async Task<string> PostAsync(string endpoint, HttpContent content, Dictionary<string, string> headers = null, AuthenticationHeaderValue auth = null)
         {
// add any custom headers to the client if provided 
if (headers != null)
{
    foreach (var header in headers)
    {
        client.DefaultRequestHeaders.Add(header.Key, header.Value);
    }
}
// add any authentication header to the client if provided 
if (auth != null)
{
    client.DefaultRequestHeaders.Authorization = auth;
}
// send a POST request to the endpoint with the content and get the response 
HttpResponseMessage response = await client.PostAsync(endpoint, content);
response.EnsureSuccessStatusCode();

// read the response content as a string and return it 
string responseBody = await response.Content.ReadAsStringAsync();
return responseBody;
}

// define a generic method to send a PUT request asynchronously and return the response as a string 
private static async Task<string> PutAsync(string endpoint, HttpContent content, Dictionary<string, string> headers = null, AuthenticationHeaderValue auth = null)
{
// add any custom headers to the client if provided 
if (headers != null)
{
    foreach (var header in headers)
    {
        client.DefaultRequestHeaders.Add(header.Key, header.Value);
    }
}// add any authentication header to the client if provided 
if (auth != null)
{
    client.DefaultRequestHeaders.Authorization = auth;
}
// send a PUT request to the endpoint with the content and get the response 
HttpResponseMessage response = await client.PutAsync(endpoint, content);
response.EnsureSuccessStatusCode();

// read the response content as a string and return it 
string responseBody = await response.Content.ReadAsStringAsync();
return responseBody;
}

// define a generic method to send a DELETE request asynchronously and return the response as a string 
private static async Task<string> DeleteAsync(string endpoint, Dictionary<string, string> headers = null, AuthenticationHeaderValue auth = null)
{
// add any custom headers to the client if provided 
    if (headers != null)
    {
        foreach (var header in headers)
        {
            client.DefaultRequestHeaders.Add(header.Key, header.Value);
        }
    }
// add any authentication header to the client if provided 
    if (auth != null)
    {
        client.DefaultRequestHeaders.Authorization = auth;
    }
// send a DELETE request to the endpoint and get the response 
    HttpResponseMessage response = await client.DeleteAsync(endpoint);
    response.EnsureSuccessStatusCode();

// read the response content as a string and return it 
    string responseBody = await response.Content.ReadAsStringAsync();
    return responseBody;
}
    }
}

```
