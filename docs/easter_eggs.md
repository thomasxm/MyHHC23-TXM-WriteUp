# Easter Eggs

# BONUS! Fishing Guide and Mastery

**Difficulty**: :fontawesome-solid-star::fontawesome-solid-star::fontawesome-solid-star::fontawesome-solid-star::fontawesome-solid-star:<br/>
**Direct link**: [Objective5.zip](https://.../)

## Objective

!!! question "Request"
    Catch twenty different species of fish that live around Geese Islands. When you're done, report your findings to Poinsettia McMittens on the Island of Misfit Toys.

!!! question "Request"
    Catch at least one of each species of fish that live around Geese islands. When you're done, report your findings to Poinsettia McMittens.

??? quote "Poinsettia McMittens"
    Excuse me, but you're interrupting my fishing serenity. Oh, you'd like to know how to become as good at fishing as I am?<br/>
    Well, first of all, thank you for noticing my flair for fishing. It's not just about looking good beside the lake, you know.<br/>
    The key is in the details, much like crafting the perfect toy. Observe the water, the weather, and the fish’s habits - it's a science and an art.<br/>
    Of course, it helps to have a natural charm. Fish seem to find me irresistible.<br/> Must be my sparkling personality... or maybe it's just the glitter of my allure.<br/>
    Oh, the mysteries of the aquatic life around these islands are as elusive as, well, a clever compliment. But you'll get one if you probe enough.<br/>
    Remember, patience is more than a virtue in fishing; it’s a strategy. Like waiting for the right time to use flattery, you wait for the right moment to strike.<br/>
    Go see if you can catch, say, 20 different types of fish!<br/>


## Hints

??? tip "Become the Fish"
    Perhaps there are some clues about the local aquatic life located in the HTML source code.


??? tip "I Am Become Data"
    One approach to automating web tasks entails the browser's developer console. Browsers' console allow us to manipulate objects, inspect code, and even interact with websockets.

??? tip "Fishing Machine"
    There are a variety of strategies for automating repetative website tasks. Tools such as AutoKey and AutoIt allow you to programmatically examine elements on the screen and emulate user inputs.



## Solution

### Jason 
Well, first thing first, where is [Jason](https://twitter.com/BanjoCrashland/)? 

![Fishing](../img/misc/jason.png)
![Fishing](../img/misc/jason2.png)

??? question "Jason"
    Hi, I'm Jason!
    I'm not dead. 
    I'm just soaking up the sun's gnarly vibes, bro!

```
https://2023.holidayhackchallenge.com/images/notadeadfish_large.png
https://2023.holidayhackchallenge.com/images/jason.png
```


Can you believe that I was looking into the images for something interesting? Great! I found one at Pixel island: 

```
https://2023.holidayhackchallenge.com/images/backgrounds/pixel_island_foreground.png
```
![Fishing](../img/misc/pixel_island_foreground.png)

Where is our turtle? 

```
https://2023.holidayhackchallenge.com/images/turtles.jpg
```

![Fishing](../img/misc/turtles2.png)

The [Jack Forest](https://riseoftheguardians.fandom.com/wiki/Jack_Frost_(The_Guardians_of_Childhood)?file=JackFrost-PicBookWJ.jpg) paintings by Andrew Theophilopoulos can be downloaded at: 

```
for i in $(seq 1 39); do wget "https://2023.holidayhackchallenge.com/images/art/f${i}.png"; done
```
![Fishing](../img/misc/jack2.png)

In the Access Speaker challenge, we need to "speak" a passphrase to the speaker in order to open the door. 

??? Poem "Forst Poem"
    And he whispered, 'Now I shall be out of sight;<br/>
    So through the valley and over the height.'<br/>
    And he'll silently take his way.<br/>

It is [Forst Poem](https://www.poemhunter.com/poem/the-frost/) by Hannah Flagg Gould. Hannah was a 19th-century American poet.  

Captain's Comms, we can find the following websocket:

```
{
  "type": "HELLO_ENTITY",
  "entityType": "terminal",
  "id": "capcom"
}
```
Capcom is a Japanese video game company.  


### Fishing 
User your "three" buttons (Cast Line --> Reel it in --> Reel it in turn red --> Reel it in) to manually fishing 20 fishes, and report back to Poinsettia McMittens to get your 
fishing mastery challenge! 

First open the developer tool, we can find: 

```<!-- <a href='fishdensityref.html'>[DEV ONLY] Fish Density Reference</a> --><div class="overlay"></div>```

We can either replace the minimap with heatmap in js or get the heat map using wget and do our job offline. 


```wget -r -np -k https://2023.holidayhackchallenge.com/sea/fishdensityref.html```

Python script that overlay all the heat maps: 

```bash linenums="1" hl_lines="7" title="Python Code"
import sys
from PIL import Image
import os

def overlay_images(input_directory, output_directory):
    # List all PNG files in the input directory
    files = [f for f in os.listdir(input_directory) if f.endswith('.png')]

    # Initialize a variable to hold the composite image
    composite = None

    # Loop through the files and overlay them
    for file in files:
        path = os.path.join(input_directory, file)
        image = Image.open(path).convert("RGBA")

        if composite is None:
            # First image sets the size
            composite = Image.new("RGBA", image.size)
        
        # Overlay the image
        composite = Image.alpha_composite(composite, image)

    # Create output directory if it doesn't exist
    if not os.path.exists(output_directory):
        os.makedirs(output_directory)

    # Save the final composite image
    output_path = os.path.join(output_directory, 'composite.png')
    composite.save(output_path, 'PNG')
    return output_path

if __name__ == "__main__":
    if len(sys.argv) != 3:
        print("Usage: python script.py input_directory_path output_directory_path")
        sys.exit(1)

    input_directory = sys.argv[1]
    output_directory = sys.argv[2]
    
    composite_image_path = overlay_images(input_directory, output_directory)
    print("Composite image saved as:", composite_image_path)

```

Heat maps with brighter spots are the places you want to catch a particular fish. If you overlay two maps together, the bright spots remain are the places where you can catch both types of fish. 

We get the one fish: 

![Terminal 111](../img/misc/composite.png)

The fish habitats! The maps below are overlay of all 171 heat maps for 171 fishes.  

![Terminal 111](../img/misc/composite1.png)
![Terminal 111](../img/misc/composite_all.png)

You will observe on pic with only one bright spot, that is THE ONE fish: Piscis Cyberneticus Skodo. We can navigate our ship to the correct bright spot to fishing using this overlayed minimap. 

We then copy and paste the Java script under /sea directory in developer tool to your favourite AI bot, then I used the following prompt: 

```Based on my Java script code I sent to you, I need you to write a client side script by utilising Java web socket to send message that check castReelBtn is visible 5 times per second. If it is visible, click it and then wait for the reelItInBtn button to turn red (which appears be a class applied to that button), once it turns red, click it immediately. Then check openpescadexBtn and see if we got a fish, if yes, output success message to console. Then back to castReelBtn and repeat this process.```

```bash linenums="1" hl_lines="7" title="JS Code to auto fishing"
// Function to check if an element is visible
function isVisible(element) {
    return element && element.style.display !== 'none';
}

// Function to check if reelItInBtn turned red
function isReelButtonRed() {
    return reelItInBtn.classList.contains('gotone');
}

// Function to check and log the caught fish
function checkAndLogFish() {
    if (isVisible(openpescadexBtn)) {
        openpescadexBtn.click(); // Open the Pescadex

        // Assuming fish name is stored in some element after opening Pescadex
        // Replace 'fishNameElement' with the correct identifier for your application
        const fishNameElement = document.querySelector('selector-for-fish-name'); 
        if (fishNameElement) {
            console.log(`Success! Caught a ${fishNameElement.textContent}`);
        }

        // Continue with the fishing process
        setTimeout(autoFish, 500); // Adjust delay as needed
    }
}

// Function to perform the fishing action
function autoFish() {
    if (isVisible(castReelBtn)) {
        castReelBtn.click(); // Click the cast reel button

        // Wait for the reelItInBtn to turn red
        const reelInterval = setInterval(() => {
            if (isReelButtonRed()) {
                clearInterval(reelInterval);
                reelItInBtn.click(); // Click the reel in button

                // Check for caught fish
                setTimeout(checkAndLogFish, 1000); // Adjust delay as needed
            }
        }, 200); // Check for the red button 5 times per second
    }
}

// Start the auto fishing process
autoFish();
```

Run the script on your developer console and your fishing crew will fishing for you for free! To track what we had in our bucket, use the following Java code: 


```bash linenums="1" hl_lines="7" title="JS Code to downlaod fish list"

function downloadFishNames() {
    if (!playerData || !Array.isArray(playerData.fishCaught)) {
        alert("No fish data available.");
        return;
    }

    // Include the fish's name and hash in the output
    let fishNames = playerData.fishCaught.map(fish => `${fish.name} - ${fish.hash}`).join('\n');
    let blob = new Blob([fishNames], { type: 'text/plain' });
    let url = window.URL.createObjectURL(blob);
    
    let a = document.createElement('a');
    a.href = url;
    a.download = 'fish-names.txt';
    a.style.display = 'none';
    document.body.appendChild(a);
    a.click();
    window.URL.revokeObjectURL(url);
    document.body.removeChild(a);
}

// Call this function to prompt the user to download the file
downloadFishNames();
```

Once you completed the challenges, you can download every fish picture using the code below in web console: 

```bash linenums="1" hl_lines="7" title="JS Code to download all fish pics"
function downloadFishImages() {
    if (!playerData || !Array.isArray(playerData.fishCaught)) {
        alert("No fish data available.");
        return;
    }

    playerData.fishCaught.forEach(fish => {
        const imageUrl = `assets/fish/${fish.hash}.png`;
        const a = document.createElement('a');
        a.href = imageUrl;
        a.download = `${fish.name}.png`;
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
    });
}

downloadFishImages();
```

Isn't it nice to have all the fishes in your bucket?


### Images

![Fishing](../img/misc/fish_result.png)

![Fishing](../img/misc/fish2.png)

!!! success "Answer"
    170 fishes plus a special one!  

#### Websocket: 

‘Oh Hi Mark’, I have to Google it to find out this one. Then I realised ```WS_OHHIMARK``` has been in HHC for many years! [Oh Hi Mark](https://www.youtube.com/watch?v=aekfPU0SwNw)

[AUF_WIEDERSEHEN](https://en.wikipedia.org/wiki/Auf_Wiedersehen,_Pet) means farewell in German. 

If we check AAANNNDD_SCENE while we are at Rudolph's Rest Resort, 

https://2023.holidayhackchallenge.com/images/fabric/ci-rudolphsrest_floor.png

We can get an area map of the place! The area map can be a perfect tool to make a game guide. 

And Chort? 

OOOH SPARKLY seems to be from The Secret of NIMH. 

Under WS_USERS, we can see some weird usernames, interesting...

Well, when I log off from chrome browser and log in the game from Firefox, I received a new response of type: [DENNIS_NEDRY](https://jurassicpark.fandom.com/wiki/Dennis_Nedry)

Dennis Nedry was a computer programmer at Jurassic Park and a minor antagonist. 


![WebSocket](../img/misc/easter_eggs.png)

![WebSocket](../img/misc/area_map.png)

The grid section in websocket contains spaces and 1s. They are the layout of the area map. By modifying the spaces to 1s, you can enter some areas you are not suppose to be in...

![WebSocket](../img/misc/grid1.png)

#### Islands

Film Noir refers to a specific genre. Examples of noir films include 'The Black Dahlia' and 'Sin City'. An example of a game in this style is L.A. Noire.

The Island of Misfit Toys' might refer to the film 'Rudolph the Red-Nosed Reindeer & the Island of Misfit Toys'. It is noteworthy that in 'Tarnished Trove' at Misfit Toys Island, the background music is distorted. You will hear sounds like the Windows startup sound, phone interference, internet dial-up, Windows warning messages, and various other sound effects.

'Pixel Island' is a nostalgic name, reminding us that everything was made of pixels in older times.

Steampunk in gaming is a genre that combines historical elements, often from the Victorian era or a similarly industrialized setting, with futuristic technology powered by steam. This genre is characterized by its inventive and often fantastical interpretation of technology, featuring gears, airships, and analog machines, all set in a retro-futuristic world. The visual style often blends old-world elegance with mechanical innovation, creating a unique and immersive experience.

The steampunk games I can think of are: [Final Fantasy 6](https://www.ign.com/wikis/final-fantasy-vi/Walkthrough) and [Bioshock](https://steampunk.fandom.com/wiki/BioShock). 


I believe the overall theme of this year is Retro！ 

#### GameBoy or NDS?

Speaking about retro games, I used 'Lameboy' to emulate a Game Boy environment on my Nintendo DS. Here it goes: 

![Gameboy](../img/misc/gb3.png)
![Gameboy](../img/misc/gb4.png)
![Gameboy](../img/misc/gb5.png)

Classic never dies! 


#### Some random stuffs

Under the js/main folder in developer tool we can find many interesting avatars that were used in previous HHC. They were really interesting.  

```https://2023.holidayhackchallenge.com/images/avatars/cyberus.png```
![avatars](../img/misc/cyberus.png)
```https://2023.holidayhackchallenge.com/images/avatars/trolls/8cf69b0ce8ba414e8f7741dddb785626.png```
![avatars](../img/misc/8cf69b0ce8ba414e8f7741dddb785626.png)

## Response

!!! quote "Poinsettia McMittens"
    Hoy small fry, nice work!

    Now, just imagine if we had an automatic fish catcher? It would be as ingenious as me on a good day!

    I came across this fascinating article about such a device in a magazine during one of my more glamorous fishing sessions.

    If only I could get my hands on it, I'd be the undisputed queen of catching them all!

    You managed to catch every fish? You're like the fishing version of a Christmas miracle!

    Now, if only you could teach me your ways... but then again, I'm already pretty fabulous at everything I do.
