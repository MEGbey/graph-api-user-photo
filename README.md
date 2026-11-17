# Microsoft Graph API - User Profile Photo (OAuth 2.0 PKCE + Postman)

[🇹🇷 Türkçe](#-türkçe) | [🇬🇧 English](#-english)

---

## 🇹🇷 Türkçe

Bu depo, **Microsoft Graph API** üzerinden oturum açmış kullanıcının profil fotoğrafını (`GET /v1.0/me/photo/$value`) **OAuth 2.0 Authorization Code Flow with PKCE** kullanarak çekmek için hazırlanmış Postman koleksiyonunu içerir.

### 📁 Depo İçeriği

* `Graph API - User Photo.postman_collection.json`: Tüm yetkilendirme ve API isteklerini barındıran Postman v2.1 koleksiyon dosyası.

### 🔄 Akış Adımları

1. **Get Authorization Code (`GET`):**
   * `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` uç noktasına `client_id`, `scope` (`openid profile User.Read`) ve PKCE `code_challenge` (`S256`) parametreleriyle tarayıcı üzerinden yetkilendirme isteği gönderilir.
   * Başarılı giriş sonrası yönlendirme URL'indeki (`redirect_uri`) `code` parametresi alınır.
2. **Exchange Code for Token (`POST`):**
   * `https://login.microsoftonline.com/common/oauth2/v2.0/token` uç noktasına alınan `authorization_code` ve eşleşen `code_verifier` gönderilerek `access_token` elde edilir.
3. **Get Current User Photo (`GET`):**
   * Alınan `access_token`, `Authorization: Bearer {{access_token}}` başlığıyla `https://graph.microsoft.com/v1.0/me/photo/$value` uç noktasına iletilir ve profil fotoğrafı ikili (binary) veri olarak görüntülenir.

### 🚀 Postman ile Çalıştırma

1. Postman uygulamasını veya web arayüzünü açın ve **Import** butonuna tıklayın.
2. Depodaki `Graph API - User Photo.postman_collection.json` dosyasını seçerek içe aktarın.
3. Koleksiyonun **Variables** sekmesine geçerek şu değişkenleri doldurun:
   * `authorization_code`: Yetkilendirme yönlendirmesinden elde edilen kod.
   * `access_token`: Token takası sonrası dönen Bearer erişim anahtarı.
4. Sırasıyla **Exchange Code for Token** ve **Get Current User Photo** isteklerini çalıştırın (`200 OK` yanıtı ile profil fotoğrafı görüntülenir).

---

## 🇬🇧 English

This repository contains a Postman collection configured to fetch the signed-in user's profile photo (`GET /v1.0/me/photo/$value`) from the **Microsoft Graph API** using the **OAuth 2.0 Authorization Code Flow with PKCE**.

### 📁 Repository Contents

* `Graph API - User Photo.postman_collection.json`: Postman v2.1 collection file containing the authorization and API requests.

### 🔄 Flow Steps

1. **Get Authorization Code (`GET`):**
   * Initiates an authorization request in the browser to `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` with `client_id`, `scope` (`openid profile User.Read`), and PKCE `code_challenge` (`S256`).
   * After signing in, extract the `code` query parameter from the `redirect_uri`.
2. **Exchange Code for Token (`POST`):**
   * Sends the retrieved `authorization_code` along with the matching `code_verifier` to `https://login.microsoftonline.com/common/oauth2/v2.0/token` to obtain an `access_token`.
3. **Get Current User Photo (`GET`):**
   * Calls `https://graph.microsoft.com/v1.0/me/photo/$value` with the `Authorization: Bearer {{access_token}}` header to retrieve the user's profile image as binary data.

### 🚀 How to Run in Postman

1. Open the Postman desktop app or web client and click **Import**.
2. Select and import `Graph API - User Photo.postman_collection.json` from this repository.
3. Navigate to the collection's **Variables** tab and set the following values:
   * `authorization_code`: The authorization code obtained from the browser redirect.
   * `access_token`: The Bearer access token returned from the token exchange request.
4. Run **Exchange Code for Token** followed by **Get Current User Photo** (`200 OK` returns and previews the user's profile photo).
