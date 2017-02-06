# .NET
Exemplo de integração SAFe com C# .NET.

```C#
var client = new HttpClient { BaseAddress = new Uri(urlServico) };
xclient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
var form = new FormUrlEncodedContent(new Dictionary<string, string>
{
    { "grant_type", "password" },
    { "username", username },
    { "password", password }
});

var token = client.PostAsync("token", form).Result;

var result = (Newtonsoft.Json.Linq.JObject)Newtonsoft.Json.JsonConvert.DeserializeObject(token.Content.ReadAsStringAsync().Result);
client.DefaultRequestHeaders.Add("Authorization", string.Format("Bearer {0}", result["access_token"]));
HttpResponseMessage response = client.PostAsJsonAsync("api/Pedido", pedido).Result;
return response.IsSuccessStatusCode
        ? response.ReasonPhrase
        : string.Format("{0} ({1}) - {2}",
            (int)response.StatusCode, response.ReasonPhrase, response.Content.ReadAsStringAsync().Result);
```
