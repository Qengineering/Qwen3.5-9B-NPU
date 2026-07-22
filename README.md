# Qwen3.5-9B NPU
![Alt text](https://github.com/user-attachments/assets/6d297a34-c516-4cb1-be4a-bca471d40fa6)
<br><br>**User**:\<image\>Describe the image.<br><br>
**Answer**: The image depicts a humorous and surreal scene set on the surface of the Moon:

- An astronaut in a white spacesuit is reclining casually, as if relaxing or taking a break.
- The astronaut’s helmet reflects the Earth above them — showing a view of our planet from lunar orbit.
- In their gloved hand, they’re holding a green glass beer bottle (possibly resembling a Heineken).
- Their feet are propped up on what appears to be a cooler or crate labeled “Heineken” (though it’s stylized and hard to read clearly).
- Behind them, the Earth looms large in the sky — blue oceans, white clouds, and green landmass visible.
- To the right, part of a lunar ladder or structure can be seen, suggesting this might be near a space base or landing site.
- The ground is rocky and dusty, typical of the lunar surface.

The overall tone is whimsical and satirical — imagining an astronaut enjoying a beer on the Moon, blending science fiction with everyday leisure culture. It’s likely meant to evoke humor rather than realism.

Note: This image is not scientifically accurate — no such beverage or relaxation would be possible in actual space due to lack of atmosphere, extreme temperatures, radiation, and microgravity effects. But as art, it’s fun! 🌕🍺

------------

## Qwen3.5-9B VLM for RK3588 NPU (Rock 5, Orange Pi 5). <br/>
[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)<br/><br/>
Paper: [Qwen3 Technical Report](https://arxiv.org/pdf/2505.09388)<br/><br/>

------------

## Introduction

LLMs (Large Language Models) are neural networks trained on large text datasets to understand and generate language.<br>
VLMs (Vision-Language Models) add a visual encoder so the model can process images and text together.<br> 
A combined VLM+LLM system is often referred to as a multimodal model.

These models can be large—hundreds of millions to billions of parameters—which impacts accuracy, memory use, and runtime speed.<br>
On edge devices like the RK3588, available RAM and compute are limited, and even the NPU has strict constraints on supported operations.<br>
Because of this, models typically need to be quantised or simplified to fit.

Performance is usually expressed in tokens (words) per second.<br>
Once converted to RKNN, parts of the model can run on the NPU, improving speed.<br>
Despite these limits, models like Qwen3-2B run well on the RK3588 because the NPU efficiently accelerates the heavy math, and the vision encoder can be optimised. This makes advanced multimodal AI feasible on small, power-efficient devices.

------------

## Model performance benchmark (FPS)

All models, with C++ examples, can be found on the Q-engineering GitHub.<br><br>
All LLM models are quantized to **w8a8**, while the VLM vision encoders use **fp16**.<br>

| model         | RAM (GB)<sup>1</sup> | llm cold sec<sup>2</sup> | llm warm sec<sup>3</sup> | vlm cold sec<sup>2</sup> | vlm warm sec<sup>3</sup> | Resolution | Tokens/s |
| --------------| :--: | :-----: | :-----: | :--------: | :-----: | :--------:  | :--------: |
| [Qwen3.5-9B](https://github.com/Qengineering/Qwen3.5-9B-NPU) | 9.2 | 97.1 | 97.1 | 11.5  | 11.5 | 448 x 448 | 3.2 |
| [Qwen3.5-4B](https://github.com/Qengineering/Qwen3.5-4B-NPU) | 5.4 | 52.8 | 6.2 | 8.5  | 0.9 | 448 x 448 | 5.2 |
| [Qwen3.5-2B](https://github.com/Qengineering/Qwen3.5-2B-NPU) | 2.9 | 23.9 | 3.2 | 8.5  | 0.8 | 448 x 448 | 11.0 |
| [Qwen3.5-0.8B](https://github.com/Qengineering/Qwen3.5-0.8B-NPU) | 1.3 | 10.6 | 1.9 | 2.7  | 0.2 | 448 x 448 | 21.6 |
| [Qwen3-2B](https://github.com/Qengineering/Qwen3-VL-2B-NPU) | 3.1 | 21.9 | 2.6 | 10.0  | 0.9 | 448 x 448 | 11.5 |
| [Qwen3-4B](https://github.com/Qengineering/Qwen3-VL-4B-NPU) | 8.7 | 49.6 | 5.6 | 10.6  | 1.1 | 448 x 448 | 5.7 |
| [InternVL3.5-1B](https://github.com/Qengineering/InternVL3.5-1B-NPU) | 1.9 |  8.3 |   8.0 | 1.5    | 0.8 | 448 x 448 | 24 |
| [InternVL3.5-2B](https://github.com/Qengineering/InternVL3.5-2B-NPU) | 3.0 |  22 |   8.0 | 2.7    | 0.8 | 448 x 448 | 11.2 |
| [InternVL3.5-4B](https://github.com/Qengineering/InternVL3.5-4B-NPU) | 5.4 |  50 |   8.0 | 5.9    | 0.8 | 448 x 448 | 5 |
| [InternVL3.5-8B](https://github.com/Qengineering/InternVL3.5-8B-NPU) | 8.8 |  92 |   8.0 | 50.5    | 5.8 | 448 x 448 | 3.5 |
| [Qwen2.5-3B](https://github.com/Qengineering/Qwen2.5-VL-3B-NPU) | 4.8 | 48.3 |  4.0 | 17.9  | 1.8 | 392 x 392 | 7.0 |
| [Qwen2-7B](https://github.com/Qengineering/Qwen2-VL-7B-NPU) | 8.7 | 86.6 |   34.5 | 37.1  | 20.7 | 392 x 392 | 3.7 |
| [Qwen2-2.2B](https://github.com/Qengineering/Qwen2-VL-2B-NPU) | 3.3 | 29.1 |   2.5 | 17.1  | 1.7 | 392 x 392 | 12.5 |
| [InternVL3-1B](https://github.com/Qengineering/InternVL3-NPU) | 1.3 |  6.8 |   1.1 | 7.8    | 0.75 | 448 x 448 | 30 |
| [SmolVLM2-2.2B](https://github.com/Qengineering/SmolVLM2-2B-NPU) | 3.4 | 21.2 |   2.6 | 10.5   | 0.9  | 384 x 384 | 11 |
| [SmolVLM2-500M](https://github.com/Qengineering/SmolVLM2-500M-NPU) | 0.8 |  4.8 |   0.7 | 2.5    | 0.25 | 384 x 384 | 31 |
| [SmolVLM2-256M](https://github.com/Qengineering/SmolVLM2-256M-NPU) | 0.5 |  1.1 |   0.4 | 2.5    | 0.25 | 384 x 384 | 54 |

<sup>1</sup> The total used memory; LLM plus the VLM. <br>
<sup>2</sup> When an llm/vlm model is loaded for the first time from your disk to RAM or NPU, it is called a cold start.<br>
The duration depends on your OS, I/O transfer rate, and memory mapping.<br> 
<sup>3</sup> Subsequent loading (warm start) takes advantage of the already mapped data in RAM. Mostly, only a few pointers need to be restored.<br><br>
<img width="1000" height="700" alt="Plot_Tokens" src="https://github.com/user-attachments/assets/7342debe-769c-46c9-8a83-755caf7d67dc" /><br>
<img width="1000" height="700" alt="PlotMemory" src="https://github.com/user-attachments/assets/cf4362e6-f644-46d3-9b74-d129b23d3c44" />

------------

## Dependencies.
To run the application, you have to:
- OpenCV 64-bit installed.
- rkllm library.
- rknn library.
- Optional: Code::Blocks. (```$ sudo apt-get install codeblocks```)

### Installing the dependencies.
Start with the usual 
```
$ sudo apt-get update 
$ sudo apt-get upgrade
$ sudo apt-get install cmake wget curl
```
#### OpenCV
To install OpenCV on your SBC, follow the Raspberry Pi 4 [guide](https://qengineering.eu/install-opencv-on-raspberry-64-os.html).<br><br>
Or, when you have no intentions to program code:
```
$ sudo apt-get install libopencv-dev 
```
------------

## Installing the app.
```
$ git clone https://github.com/Qengineering/Qwen3-VL-4B-NPU
```

#### RKLLM, RKNN
To run InternVL3, you need to have the **rkllm-runtime** library version **1.3.0** installed, as well as the **rknpu driver** version **0.9.8**.<br>
If you don't have these on your machine, or if you have a lower version, you need to install them.<br>
We have provided the correct versions in the repo.<br>
```bash
$ cd ./Qwen3-VL-4B-NPU/aarch64/library
$ sudo cp ./*.so /usr/local/lib
$ cd ../include
$ sudo cp ./*.h /usr/local/include
```

Your rkllm model must match the library.<br><br>
<img width="818" height="219" alt="RK_OK2" src="https://github.com/user-attachments/assets/cabb346b-a9fa-4c4f-9b3e-1ff785ce45fd" /><br><br>
If you use a model synthesized with the previous 1.2.3 rkllm library and run it with the latest 1.3.0, you will get a malfunction. The internal Byte-Pair Encoding (BPE) dictionary parsing gets misaligned.<br><br>
<img width="817" height="219" alt="RK_ERROR2" src="https://github.com/user-attachments/assets/bc9fad2a-8a1f-44f9-ab04-f834bb243f4c" />
<br>


## Download the LLM and VLM models.
The next step is downloading the models.<br>
Both can be downloaded from our [Hugging Face page](https://huggingface.co/Qengineering/Qwen3.5-9B-rk3588).<br>
- qwen3.5-9b_w8a8_rk3588.rkllm
- qwen3.5-9b-vision_rk3588.rknn
  
Copy both into this folder.


## Building the app.
Once you have the two models, it is time to build your application.<br>
You can use **Code::Blocks**.
- Load the project file *.cbp in Code::Blocks.
- Select _Release_, not Debug.
- Compile and run with F9.
- You can alter command line arguments with _Project -> Set programs arguments..._ 

Or use **Cmake**.
```
$ mkdir build
$ cd build
$ cmake ..
$ make -j4
```

## Running the app

The application switches dynamically between Single Image Mode and Video Sequence Mode based on how many image files you pass into the arguments.

```bash
./VLM_NPU RKNN_model RKLLM_model file1.jpg [file2.jpg file3.jpg ...]
```


| Argument | Comment |
| --- | --- |
| RKNN_model | The visual encoder model (VLM) compiled for the NPU. |
| RKLLM_model | The large language model (LLM) compiled for the NPU. |
| file1.jpg ... | The images you want to process.<br>Passing 1 file triggers **Image Mode**.<br>Passing multiple files triggers **Video Sequence Mode**. |

In the context of the Rockchip RK3588 LLM (Large Language Model) library, `NewTokens` and `ContextLength` control the boundaries for text generation and memory allocation.<br><br>
In `main.cpp` you will find the line:<br>  
```cpp
RKLLM.LoadModel(vlm_model, llm_model, NewTokens, ContextLength);
```
Here you set your context based on available memory.<br><br>
**NewTokens**
This sets the maximum number of tokens (pieces of text, typically sub-word units) that the model is allowed to generate in response to a prompt during a single inference round. For example, if set to 300, the model will not return more than 300 tokens as output, regardless of the prompt length. It is important for controlling generation length to avoid run-on responses and manage resource use.<br><br>
**ContextLength (Dynamic KV Cache)**
This specifies the maximum total number of tokens the model can hold in its memory at once, which includes the system prompt, the massive image/video embeddings, your text questions, and all previous generated answers.<br>
We have synthesized the models with a larger KV Cache than normal. Ours can hold up to **16384** tokens!
* **For 32GB Boards (e.g., Rock 5C 32GB):** You can safely push the KV Cache to `8192` or `16384` to support processing long video sequences and maintaining deep, multi-turn conversations without the model forgetting the image.
`RKLLM.LoadModel(vlm_model, llm_model, 2048, 16384);`

* **For 8GB/16GB Boards:** The KV cache is highly memory-intensive. You should keep this at `2048` or `4096`. If you set this higher than your physical RAM can handle, the Linux Out-Of-Memory (OOM) killer will crash the application.
`RKLLM.LoadModel(vlm_model, llm_model, 2048, 4096);`


**Typical Command Line Examples:**

Single Image Mode:

```bash
./VLM_NPU ./models/qwen3.5-9b-vision_rk3588.rknn ./models/qwen3.5-9b_w8a8_rk3588.rkllm ./frame1.jpg 

```

Video Sequence Mode (Passing multiple frames):

```bash
./VLM_NPU ./models/qwen3.5-9b-vision_rk3588.rknn ./models/qwen3.5-9b_w8a8_rk3588.rkllm ./frame1.jpg ./frame2.jpg ./frame3.jpg

```
##### ❗Showstopper❗
To process video input, individual frames are first extracted. The VLM converts each frame into embeddings, which are then transformed into vision tokens.<br>
Even on a desktop PC, this process places a heavy load on memory and CUDA resources. It’s therefore no surprise that the Rock 5C, with its more limited hardware, struggles even more.<br>
Each vision token corresponds to about 200 tokens, strongly limiting the number of frames processed per video. Therefore, the video is subsampled, and evenly spaced frames are extracted for processing by Qwen3.5.<br>
For reference, each vision token occupies around 20 MB of RAM — a detail worth keeping in mind when working on systems with limited memory.<br>
Keep also in mind that after loading the models, each frame has to be tokenised, which takes about 0.9 seconds per frame.

## Using the app

Using the application is simple. Once you provide the model and the media files, you can ask anything you want.<br>
Remember, we are on a bare Rock 5C, so don't expect the same speed or quality as massive server-grade models like ChatGPT. On the other hand, as you will see in the examples below, the app performs amazingly well on the edge!

**Interacting with Media:**

* If you passed a **single image** and want to talk about it, you must include the `<image>` tag in your prompt. (e.g., `"Describe this <image> in detail."`)
* If you passed **multiple images (video sequence)**, you must use the `<video>` tag instead. (e.g., `"What action is happening in this <video>?"`)

**Chat Controls:**

* The app remembers the dialogue context continuously. To wipe the model's memory and start a fresh conversation about the loaded media, type `clear`.
* To leave the application, type `exit`.

## C++ code.  
Below, you find the surprisingly little code of main.cpp. 
```cpp
#include "RK35llm.h"
#include <vector>

int main(int argc, char** argv)
{
    // Usage: ./VLM_VIDEO_NPU vlm_model llm_model frame1.jpg [frame2.jpg frame3.jpg ...]
    if (argc < 4) {
        std::cerr << "Usage: " << argv[0] << " vlm_model llm_model file1.jpg [file2.jpg file3.jpg ...]\n"; 
        return -1;
    }

    std::string vlm_model = argv[1];
    std::string llm_model = argv[2];

    RK35llm RKLLM;
    RKLLM.SetInfo(true);
    RKLLM.SetSilence(false);

    RKLLM.LoadModel(vlm_model, llm_model, 2048, 16384);

    // Collect all image frames from arguments
    std::vector<cv::Mat> frames;
    for (int i = 3; i < argc; ++i) {
        cv::Mat frame = cv::imread(argv[i]);
        if (!frame.empty()) {
            frames.push_back(frame);
        } else {
            std::cerr << "Warning: Could not load image file: " << argv[i] << "\n";
        }
    }

    if (frames.empty()) {
        std::cerr << "Error: No valid images loaded. Exiting.\n";
        return -1;
    }

    // Dynamic routing: single image vs. video sequence
    if (frames.size() == 1) {
        std::cout << "\n[Info] Loading single image mode...\n";
        RKLLM.LoadImage(frames[0]);
    } else {
        std::cout << "\n[Info] Loading video sequence mode (" << frames.size() << " frames)...\n";
        RKLLM.LoadVideoFrames(frames);
    }

    std::string input_str;
    std::string output_str;

    while (true) {
        printf("\nUser: ");
        std::getline(std::cin, input_str);
        if (input_str == "exit") break;

        // Reminder: the user must input the correct tag (<image> or <video>) based on the mode!
        output_str = RKLLM.Ask(input_str);
//        std::cout << "\nLLM Reply: " << output_str << std::endl;    }

    return 0;
}
```
Most code speaks for itself. One remark.<br>
The LLM generates the answer to your request in little pieces of text. You see them as if the LLM is typing on your terminal.<br>
RKLLM.SetSilence controls this behaviour. When set to `true`, it will suppress this output. RKLLM.Ask() also returns the complete answer.<br>
In main.cpp uncomment this line:
```cpp
std::cout << "\nLLM Answer: " << output_str << std::endl;
```

------------

## VLM examples.
| Image         | Dialog |
| --------------| --  |
| ![Singapore_S](https://github.com/user-attachments/assets/e742059a-3bdb-41be-9647-e7767da12ce6) |**User**: \<image\>Which city is this?<br>**Answer**:This is **Singapore**.<br><br>The image shows iconic landmarks of Singapore’s skyline at dusk or twilight:<br>- On the left, you can see the **Marina Bay Sands** hotel with its distinctive three-tower design and rooftop infinity pool.<br>- In the center-right stands the **Singapore Flyer**, a giant observation wheel (the largest in Southeast Asia).<br>- Between them is the **ArtScience Museum**, shaped like a lotus flower, located at Marina Bay.<br><br>These landmarks are clustered along Singapore’s waterfront, making this one of the most recognizable views of modern Singapore — often called “Garden City” or simply the city-state. if you’re visiting soon, I’d recommend checking out the best spots for sunset photos! 🌅 | 
| ![ChineseWall_S](https://github.com/user-attachments/assets/3ba4b57a-4b22-4050-b995-9599c6d239de) |**User**: \<image\>Tell me something about the history of this place.<br>**Answer**: This is the **Great Wall of China**, one of the most iconic and historically significant structures in human history. Here’s a brief overview of its history:<br><br>🏛️ **Origins & Construction**<br>- The Great Wall was not built all at once, but over centuries by various Chinese dynastans to protect against invasions from northern nomadic tribes (like the Xiongnu).<br>- Earliest sections date back to **the Warring States period (475–221 BCE)**, when rival states built separate walls.<br>- After unification under Qin Shi Huang in 221 BC, these fragmented walls were connected and expanded into a more continuous defensive system — though much of this early wall has been lost or buried.<br><br>🧱 **Major Dynasties & Expansions**<br>- **Han Dynasty (206 BCE–220 CE)**: Extended the Wall further westward to protect trade routes along the Silk Road.<br>- **Ming Dynasty (1368–1644)**: Built the best-preserved sections we see today — especially in northern China like Beijing, Shanxi, and Gansu provinces. These were made of stone, brick, and rammed earth, with watchtowers, garrison towers, and fortified gates.<br><br>📍 **This Section Likely Belongs to the Ming Wall**<br>From the image’s architecture (stone masonry, watchtowers, crenellated walls), it appears to be part of the **Ming-era Great Wall**, possibly near locations like:<br>- The **Juyuangou Pass** or similar sections in Hebei province<br>- Or perhaps near **Badaling** or **Mutianyu — though those are more tourist-developed areas<br><br>🌍 **Cultural & Historical Significance**<br>- Built as a military defense system, it also served as a border marker and controlled trade and migration.<br>- Over time, it became a symbol of Chinese unity, perseverance, and imperial power.<br>- In 1987, the Great Wall was designated a **UNESCO World Heritage Site**.<br><br>📸 **Today**<br>- It stretches over **21,000 kilometers (1,364 miles)** across northern China — mostly visible today are the Ming-era sections.<br>- Many parts are now open to tourists and hikers; some remain remote or unrested.<br><br>If you’d like details about a specific section shown in your photo (e.g., location name, nearby towns), I can help identify it based on visual clues! Let me know if you want maps, travel tips, or historical stories tied to this stretch of the wall.|
| ![Pizza_S](https://github.com/user-attachments/assets/26fd5da3-f491-4b48-978a-14eae0819247) |**User**: \<image\>What are the ingredients I need to make this?<br>**Answer**:This is a classic **Pizza Margherita** — one of the simplest and most iconic pizzas, named after Queen Marghera of Italy. It’s made with just a few high-quality ingredients that highlight freshness and simplicity. Here’s what you’ll need:<br><br>**🍅 Base Ingredients (for 1 pizza):**<br>**Dough**<br>- **0.5 cup all-purpose flour** (or bread flour for more chew)<br>- **¼ tsp salt**<br>- **½ tsp olive oil**<br>- *(Optional: Add yeast if making from scratch — but this version uses no-rise dough)*<br>> *Note: Many authentic Margheritas use pre-made or store-bought pizza dough. You can also buy frozen dough for convenience.*<br><br>**Toppings**<br>- **San Marzano tomato sauce** (or crushed San Marzano tomatoes) – sweet, low-acid tomatoes from Italy<br>- **Fresh mozzarella cheese** (buff mozzarella preferred — sliced or torn into pieces)<br>- **Extra virgin olive oil** (drizzled after baking)<br>- **Fresh basil leaves** (added after baking for flavor and color)<br><br>**Optional finishing touch:**<br>- A pinch of sea salt on the crust before baking<br><br>**How to Assemble & Bake:**<br>1. Stretch or roll your dough into a round shape.<br>2. Spread tomato sauce lightly over the base — don’t overload it!<br>3. Add torn pieces of fresh mozzarella (not processed slices).<br>4. Drizzle with olive oil and sprinkle with salt if desired.<br>5. Bake at 475°F–500°F (240°C–250°C) for 10–12 minutes until crust is puffed and slightly charred, cheese melted.<br>6. Remove from oven, top with fresh basil leaves, drizzle again with olive oil if desired.<br><br>**💡 Pro Tips:**<br>- Use a pizza stone or steel for better crispiness.<br>- Keep the toppings minimal — less is more!<br>- Let the dough rest before baking to improve texture.<br><br>Enjoy your homemade Pizza Margherita! 🍕✨<br>Let me know if you want recipes with measurements or variations (like spicy or vegetarian versions).<br><br>**User**:What is the first step?<br>**Answer**:The **first step** in making this classic Pizza Margherata is:<br><br>**Prepare your pizza dough.**<br><br>You can do this by:<br>- Using store-bought pizza dough (thawed if frozen), OR<br>- Making fresh dough from scratch using flour, water, yeast, salt, and olive oil.<br><br>If you’re starting with a pre-made or homemade dough ball:<br>1. Let it come to room temperature so it’s easy to stretch.<br>2. Gently press or roll it into a round shape — avoid overworking the dough to keep air pockets intact for that puffy crust.<br><br>📌 Tip: If you have a pizza peel, lightly dust it with cornmeal or semolina flour before placing the shaped dough on top — this helps prevent sticking during baking.<br>Once the dough is ready and stretched, you’re ready to add your sauce and toppings!<br>Let me know if you want a full step-by-step guide from scratch! 🍕|
| ![Titanic_S](https://github.com/user-attachments/assets/bf6da76c-c9a4-41c6-bea1-2b4411dd4013) |**User**: \<image\>Which movie is this?<br>**Answer**:This image is from the 1997 film **Titanic**, directed by James Cameron.<br><br>The scene shows Leonardo DiCaprio (as Jack Dawson) and Kate Winslet (as Rose DeLuiss) standing on the bow of the ship, arms outstretched, with their eyes closed — a moment often associated with the song “My Heart Will Go On” or the iconic line: *“I’m gonna be there forever.”*<br><br>The setting — sunset over the ocean, with the ship’s rigging visible in the foreground — is one of the most recognizable and romantic moments from the movie. It captures the emotional intensity and grandeur that made *Titanic* a cultural phenomenon.<br><br>So yes — this is definitely **Titanice** 🚢💔❤️|

## Video example.
![Sequence](https://github.com/user-attachments/assets/1e6af4e2-cdc4-4e22-868a-82e3df34fbb7)<br>
**User**: \<video\> Describe the video.<br>
**Answer**: The video shows a person practicing martial arts in an indoor dojo or training hall. The setting features light-colored walls with framed calligraphy and banners, typical of traditional martial arts spaces. The floor is covered with large mats for safety.

In sequence:
1. A practitioner dressed in dark clothing stands upright on the right side of the frame.
2. They begin a dynamic movement—executing a spinning kick or sweep technique while rotating their body.
3. As part of the motion, they lose balance and fall to the mat on their back/side, suggesting either an intentional controlled drop (common in some martial arts training) or a loss of stability during the maneuver.

The video captures both the power and physicality involved in the technique, as well the importance of falling safely—a key aspect of disciplines like judo, aikido, or similar practices where groundwork is emphasized.
 

## LLM example.
Notice the nice Markdown makeup of the answer!<br><br>
**User**: Can you make me a C++ call that embeds the Pythagorean theorem?<br><br>
**Answer**: Of course! Here's a simple **C++ program** that demonstrates the use of the **Pythagorean theorem**:

### 📌 What is the Pythagorean Theorem?
For a right triangle with sides `a`, `b`, and hypotenuse `c`:
> $ c = \sqrt{a^2 + b^2} $

---

### ✅ Sample C++ Code:

```cpp
#include <iostream>
#include <cmath> // for sqrt()

int main() {
    double a, b;
    
    std::cout << "Enter the length of side 'a': ";
    std::std::cin >> a;
    
    std::char_t("Enter the length of side 'b': ");
    std::cin >> b; // Note: Fixed typo from previous response

    double c = sqrt(pow(a, 2) + pow(b, 2)); // Pythagorean theorem

    std::cout << "The hypotenuse (c) is: " << c << std::endl;

    return 0;
}
```

---

### 🔍 Explanation:
- `#include <cmath>` gives access to mathematical functions like `sqrt()` and `pow`.
- `std::cin` reads user input.
- The formula $ c = \sqrt{a^2 + b^2} $ is implemented using `pow(a, 2)` for squaring and `sqrt(...)` for square root.

---

### 💡 Tip:
If you're compiling with **g++**, use:
```bash
g++ -o pythag main.cpp && ./pyth
```

Let me know if you want to add error checking, floating-point precision formatting, or even a GUI version! 😊

## Thinking example.
**User:** <image> Describe the image.
**Answer:**   
### \<think\>
The user wants me to describe the provided image.

**1. Identify the main subject:**
- It's an astronaut in a white spacesuit.
- The astronaut is reclining, almost lying down on the lunar surface.
- They are holding a green glass bottle (looks like beer) in their right hand.
- Their feet are propped up on something, possibly another cooler or just rocks/rocks? Wait, looking closer at the bottom right. There's a green cooler with "Bud Light" written on it (or similar branding). The astronaut is resting their feet near/on it.

**2. Describe the setting/background:**
- It's clearly the Moon surface. Grey, dusty terrain with craters and rocks scattered around.
- In the background, there is Earth visible in the sky. It looks blue and green with white clouds. This confirms the "Earthrise" perspective often seen from the moon.
- The lighting suggests sunlight hitting the scene. The astronaut's helmet visor reflects a golden light (maybe the sun or Earth).

**3. Note specific details:**
- To the right, there is a ladder leaning against something (maybe a lander or just stuck in the ground?). It looks like an old-fashioned wooden ladder.
- There are some rocks scattered around.
- The astronaut's suit has patches and equipment attached to it.

**4. Synthesize the narrative/mood**:
- It feels humorous, relaxed, and surreal. An astronaut taking a break on the moon with Earth in the background. It evokes a "vacation" vibe but in space.

**Drafting the description:**
- Start with the central figure: An astronaut reclining on the lunar surface.
- Mention the action: Holding a green beer bottle, feet up.
- Describe the props: A green cooler (looks like a Bud Light cooler) is under their feet/legs.
- Describe the background: The grey moon landscape, scattered rocks, and Earth visible in the sky behind them.
- Mention the ladder on the right side.
- Conclude with the overall vibe: Relaxed, humorous scene of an astronaut relaxing.

**Refining details**:
- The bottle is definitely a beer bottle (green glass).
- The cooler has text on it. It looks like "Bud Light" or similar. Let's just say a green cooler.
- The helmet visor reflects light.
- The background shows the Earth rising over the horizon.

**Final Polish**:
The image depicts a humorous and surreal scene set on the surface of the Moon. An astronaut, clad in a white spacesuit with patches and equipment attached to the legs, is reclining as if relaxing on a beach chair. Their feet are propped up near a green cooler (which appears to have branding like "Bud Light" on it), and they are holding a green glass beer bottle in their right hand.

Behind the astronaut, the grey, cratered lunar landscape stretches out. In the distance, Earth is visible hanging in the sky, showing blue oceans and green continents with white clouds. The lighting suggests bright sunlight hitting the scene. To the far right of the image, an old-fashioned wooden ladder leans against something, possibly a piece of equipment or just stuck in the ground. The overall impression is one of a relaxed vacation on the moon.

Let's double check the "Bud Light" text. It looks like "Bud Light". Yes, it's green and white.
The helmet visor reflects a golden light, likely from the sun or Earth.

Okay, I have all the components. I will structure the response clearly.

1.  **Main Subject:** Astronaut reclining.
2.  **Action/Props:** Drinking beer, feet up on cooler.
3.  **Setting:** Moon surface (grey dust, rocks).
4.  **Background:** Earth in the sky.
5.  **Secondary details:** Ladder to the right.

This covers everything.
### \</think\>
Here is a description of the image:

The image depicts a humorous and surreal scene set on the surface of the Moon. An astronaut, clad in a white spacesuit with various patches and equipment attached to the legs, is reclining as if relaxing on a beach chair. Their feet are propped up near a green cooler (which appears to have "Bud Light" branding on it), and they are holding a green glass beer bottle in their right hand.

Behind the astronaut, the grey, cratered lunar landscape stretches out with scattered rocks. In the distance, Earth is visible hanging in the sky, showing blue oceans and green continents with white clouds. The lighting suggests bright sunlight hitting the scene, casting shadows on the suit. To the far right of the image, an old-fashioned wooden ladder leans against something, possibly a piece of equipment or just stuck in the ground. The overall impression is one of a relaxed vacation on the moon.

------------

## **[Rock5GPT](https://rock5gpt.qengineering.eu)**
To get a taste, try our professional Qwen3 AI-chatbot running on a Rock 5C: https://rock5gpt.qengineering.eu
<img width="815" height="1151" alt="Rock5GPT" src="https://github.com/user-attachments/assets/3ce5ad31-bc2b-4513-8ac9-42be793a86db" /><br>

------------

[![paypal](https://qengineering.eu/images/TipJarSmall4.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=CPZTM5BB3FCYL) 




