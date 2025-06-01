# Challenge Write-up: Flags are Ciphered

**Category: Forensics**

**Difficulty: Medium**

### Challenge Description


Welcome to "Flags are Ciphered"! In this challenge, you are presented with a web application displaying flags of nearly every country in the world. However, there's a subtle anomaly: one of the flags displayed belongs to a country that does not exist. Your task is to identify this peculiar flag. Upon clicking it, you will receive a cryptic hint that will guide you to the next stage of the challenge. This hint will lead you to a specific flag – the Israeli flag – which has been intentionally grey-scaled. The final answer to this challenge is cleverly encoded within this grey-scaled image using steganography.

Good luck, and happy hunting!

**Hint**

"Where no border holds its sway, A cryptic banner leads the way"

**Solution Steps**

**Step 1: Identify the Non-Existent Flag**
Access the Web Application: Navigate to the provided URL for the "Flags are Ciphered" web app.

**Visual Inspection:** Carefully browse through all the flags displayed. Look for any flag that seems out of place, unfamiliar, or simply doesn't correspond to a real-world country. This might require some general knowledge of world flags or a quick search for unfamiliar designs.

**Click the Anomaly:** Once you identify the flag of the non-existent country (e.g., a flag with an unusual design or a placeholder), click on it.

**Step 2: Decipher the Hint**
Receive the Hint: Upon clicking the non-existent flag, a hint will be revealed. This hint is crucial for the next step. (As an example, the hint might be: "The star of David holds the key, but its colors have faded away.")

**Interpret the Hint:** The hint will directly point you towards the "Israeli flag" and suggest that its appearance is altered (e.g., "colors have faded away" implying grey-scale).

**Step 3: Locate and Obtain the Target Image**
Find the Israeli Flag: Based on the hint, search for the Israeli flag within the web application. It should be distinctively grey-scaled compared to the other colored flags.

**Download the Image:** Right-click on the grey-scaled Israeli flag and save the image to your local machine. Note the filename (il.png).

Step 4: Extract the Hidden Data (Steganography using stepic)
Since the flag is encoded with stepic, you'll need to use a Python script leveraging the stepic library to extract the hidden data.

Install Prerequisites:
You'll need Pillow (for image manipulation) and stepic. If you don't have them installed, open your terminal or command prompt and run:

```pip install Pillow stepic```

**Create the Python Script:**

Save the following code as a Python file (e.g., decode_flag.py) in the same directory where you saved the grey-scaled Israeli flag image.

**Python**

```
from PIL import Image
import stepic

# Define the image filename (make sure this matches your downloaded file)
image_filename = 'israel_greyscale.png' # Or israel_flag.jpg, etc.

try:
    # Open the image using Pillow
    img = Image.open(image_filename)

    # Attempt to decode the hidden message using stepic
    # stepic typically works with LSB steganography and doesn't usually
    # require a passphrase unless it's a custom implementation on top of it.
    decoded_bytes = stepic.decode(img)

    # Print the decoded message, assuming it's UTF-8 text
    print("--- Hidden Message Found ---")
    print(decoded_bytes.decode('utf-8'))
    print("----------------------------")

except FileNotFoundError:
    print(f"Error: The image file '{image_filename}' was not found. Make sure it's in the same directory as the script.")
except Exception as e:
    print(f"An error occurred during decoding: {e}")
    print("Could not find hidden data or incorrect format. Ensure the image is valid and encoded with stepic.")
```

**Run the Script:**
Open your terminal or command prompt, navigate to the directory where you saved both the script and the image, and then run:

```python decode_flag.py```


**Retrieve the Flag**: Open the extracted file. It will contain the flag for the challenge.

**Example Flag Format:** FLAG{Th1s_1s_th3_H1dd3n_Fl4g!}