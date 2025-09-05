# pybakong

Python SDK for Cambodia Bakong Open API.  

"This Repo is built for learning purposes only." 
---

## Installation

pip install pybakong

```bash

from pybakong import BakongClient, BakongAPIError

# Initialize the client
client = BakongClient()

try:
    # Step 1: Request a token (you will receive a verification code via email)
    response = client.request_token("your@email.com", "MyOrg", "MyProject")
    print("Token Request Response:", response)

    # Step 2: Verify the token using the code from email
    token = client.verify_token("123456")
    print("Verified Token:", token)

    # Step 3: (Optional) Renew token if needed
    token = client.renew_token("your@email.com")
    print("Renewed Token:", token)

    # Step 4: Generate a QR string for a payment
    qr_string = client.generate_qr_string(
        amount=0.2,
        currency="USD",
        receiver_bakong_id="RECEIVER_ACCOUNT_ID"
    )
    print("Generated QR String:", qr_string)

    # Step 5: Generate a deeplink from the QR string (short link)
    deeplink = client.generate_deeplink(
        qr=qr_string,
        app_icon_url="https://example.com/icon.png",
        app_name="MyApp",
        app_deep_link_callback="https://example.com/callback"
    )
    print("Generated Payment Link / Deeplink:", deeplink)

except BakongAPIError as e:
    print("Bakong API Error:", e)
