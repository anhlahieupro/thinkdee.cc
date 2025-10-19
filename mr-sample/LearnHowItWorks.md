🧭 How the App Can Work and What It Can Do


![enter image description here](/LearnHowItWorks.png)


1️⃣ Search for your favorite manga

Search for your favorite manga, or open any webpage that contains it.
For example, I’ll use this sample page as a demo:
👉 https://thinkdee.cc/mr-sample/detail

Open the page and take a look. 


2️⃣ Identify the chapter list

When you open the page, you’ll see a list of chapters (like Chapter 1, 2, 3, 4…).
If you have some basic HTML/CSS knowledge, you can use Inspect Element (available in Safari/Chrome on Mac or PC) to find the selector: body > div > div.chapter
 
 
3️⃣ Create a JS filter for chapters

To filter and display only the chapter list (via injected JS), set:

url

    https://thinkdee.cc/*/*

js code

    (function() {
      // Step 1: Select all <a> elements inside the chapter container
      const tableRows = document.querySelectorAll("body > div > div.chapter > a");
    
      // Step 2: Convert NodeList to an array and map each <a> to an object
      const rowData = Array.from(tableRows).map(row => {
        const link = row;
        const title = row.querySelector("div");
        const subtitle = "";
    
        return {
          link: link ? link.href : "",
          title: title ? title.innerText.trim() : "",
          subtitle: subtitle ? subtitle.innerText.trim() : ""
        };
      });
    
      // Step 3: Return the structured data
      return rowData;
    })();


4️⃣ Test the filter

After saving, click the Filter Chapters button again.
It should now display a clean list of chapters — without any extra website content.


5️⃣ Filter images on a chapter page

When you open a chapter page, such as
👉 https://thinkdee.cc/mr-sample/chapters/chapter.html?chapter=1

You can easily detect all images using the Filter Images button.
However, some pages contain extra images, so you can also add custom JS to extract only the images you want.

Inspect the page again (like before) and find the selector path: #images > img

Then use this code:

url

    https://thinkdee.cc/*/*/*

js code

    (function() {
      // Step 1: Select all <img> elements
      const imgs = document.querySelectorAll("#images > img");
    
      // Step 2: Extract URLs (prefer data-src if available)
      const urls = Array.from(imgs).map(img =>
        (img.getAttribute("data-src") || img.getAttribute("src") || "").trim()
      );
    
      // Step 3: Return valid URLs only
      return urls.filter(Boolean);
    })();


6️⃣ Test image filtering

After saving, click the Filter Images button again.
It should now show only the images and open Reading Mode, letting you read smoothly without distractions.


💬 Need help?

If it feels too difficult, you can ask for help in the ⁠#dev channel — hopefully someone in the community can guide you!
