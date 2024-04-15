# Onehub Kotlin Library
```
import java.io.IOException
import okhttp3.MediaType.Companion.toMediaType
import okhttp3.OkHttpClient
import okhttp3.Request
import okhttp3.RequestBody.Companion.toRequestBody

val client = OkHttpClient()

val MEDIA_TYPE = "application/json".toMediaType()

val requestBody = "{\"phoneNumbers\": \"+2547XXXXXXXX,+2547XXXXXXXX\", \"message\": \"Hello Api!\",\"senderId\":\"Onehub\"}"

val request = Request.Builder()
    .url("https://api.onehub.co.ke/v1/sms/send")
    .post(requestBody.toRequestBody(MEDIA_TYPE))
    .header("Content-Type", "application/json")
    .header("x-api-user", "API_USERNAME_HERE")
    .header("x-api-key", "API_KEY_HERE")
    .build()

client.newCall(request).execute().use { response ->
    if (!response.isSuccessful) throw IOException("Unexpected code $response")
    response.body!!.string()
}
```
# Username and API Key
You can get your username and API Key [here](https://dashboard.onehub.co.ke/account/0/user/signup).
# Request Body Parameters
`phoneNumbers` - `[Type: String]` `[Required]` - Phone numbers of the recipients in international format with the plus (+) sign. Multiple numbers should be comma-separated.

`Message` - `[Type: String]` `[Required]` - The message you want to send. Each message is counted as 160 characters long. Messages longer than 160 characters will be billed accordingly.

`Sender ID` - `[Type: String]` `[Required]` - A sender ID serves as a branding for outgoing messages, typically representing your company name. Your users will receive messages with your specified sender ID. You can apply for your sender ID on our [website](https://onehub.co.ke/).
