# Dive into the World of Generative AI

Dive into the world of generative AI and keep the spirit of innovation alive. Check out the [challenges](https://github.com/adventofmultimodalai/challenges) and [resources](https://github.com/adventofmultimodalai/resources) to start your own GenAI journey today!

<div align="center">
  <img src="https://github.com/user-attachments/assets/a719fc12-337b-429b-affe-c9508200740b" alt="Generative AI" />
</div>

Hello, AI Adventurers! Ready to navigate the exciting world of Generative AI with us? Here's everything you need to ace the [Advent of MultiModal AI](https://adventaihacks.com) hackathon:

---

Hello, AI Adventurers! Ready to navigate the exciting world of Generative AI with us? Here's everything you need to ace the [Advent of MultiModal AI](https://adventaihacks.com)) hackathon:


# GenAI GitHub Repositories

1. **GenAI Playground on Intel GPUs**  
   [GitHub Repository](https://github.com/rahulunair/genAI)  
   A set of iPython notebooks from Stable Diffusion to LLMs.

2. **Intel AI Use Cases for GenAI**  
   [GitHub Repository](https://github.com/rskasturi/usecases)  
   Key insights on GenAI applications, including Stable Diffusion, LLM inference, fine-tuning, and code generation with Intel GPUs.  

3. **Diffusion Model Serving with Ray on Intel GPUs**  
   [GitHub Repository](https://github.com/rahulunair/xpu_ray)  

4. **LLM Deployments on Intel Data Center Max Series GPUs**  
   [GitHub Repository](https://github.com/TiberAICommunity/xpu_tgi)  
   A set of deployment docs for LLM deployments using TGI.

---

3. **Intel Developer Cloud**
   
   - 🌐 Step into the [Intel Tiber AI Cloud](https://cloud.intel.com) (IDC), register for free, and access Intel Xeons CPUs and GPUs. Discover a set of curated notebooks for Stable Diffusion, LLM inference and Finetuning on Intel under the 'Gen AI Essentials' section.
   - **Each notebook will give you access to:** 
      - Jupyter Notebook: Each participant will work within a Jupyter Notebook environment, optimized for Generative AI challenges. 
      - Disk Space: Upto 30 GB per user (Depending up on capacity). 
      - GPU: Intel GPU with 48 GB (Data Center Max 1100), tailored for AI applications. 
      - CPU: 4th Gen Intel Xeon. 

---


<a name="prediction-guard"></a>
3. **Prediction Guard: Access a variety of privacy-conserving LLMs, validate outputs**
   - 🛡️ Explore [Prediction Guard Documentation](https://docs.predictionguard.com). Check out the "Getting Started" and "Using LLMs" pages to run your first text or chat completions with the Prediction Guard API or Python client.

      ```python
      import os
      import json
      import predictionguard as pg
   
      os.environ['PREDICTIONGUARD_TOKEN'] = "<your PG access token>"
   
      response = pg.Completion.create(
         model="Neural-Chat-7B",
         prompt="The advent of Gen AI hackathon is: "
      )
   
      print(json.dumps(
         response,
         sort_keys=True,
         indent=4,
         separators=(',', ': ')
      ))
      ```

   - 💪 Run through some of the examples in the [Using LLMs](https://docs.predictionguard.com/usingllms) section of the docs to learn more about basical prompting, prompt engineering, retrieval, chat, agents, etc.

---

4. **Intel Extension for PyTorch (XPUs):**
   - 🔥 Check if XPU is ready:
     ```python
     import torch
     import intel_extension_for_pytorch
     print(f"torch.xpu.is_available()")
     ```
   - 📚 Dive deeper at [Intel XPU Tutorials](https://intel.github.io/intel-extension-for-pytorch/xpu/latest/tutorials/examples.html)

---

5. **Detect Your AI Resources: The Discovery Commands**
   - 🔍 Uncover Intel GPUs and CPUs:
     ```bash
     echo "Intel GPUs:"
     xpu-smi  discovery 2> /dev/null
     echo "Intel Xeon CPU:"
     lscpu | grep "Model name"
     xpu-smi dump -m 18
     ```
---

6. **Python Package Installation: Effortlessly**
   - 📦 Streamline your installations:
     ```python
     import sys
     import site
     from pathlib import Path
     !echo "Installing..."
     !{sys.executable} -m pip cache purge > /dev/null
     !{sys.executable} -m pip install <python_package_name>
     !echo "Installation Complete."
      def get_python_version():
          return "python" + ".".join(map(str, sys.version_info[:2]))
      
      def set_local_bin_path():
          local_bin = str(Path.home() / ".local" / "bin") 
          local_site_packages = str(
              Path.home() / ".local" / "lib" / get_python_version() / "site-packages"
          )
          sys.path.append(local_bin)
          sys.path.insert(0, site.getusersitepackages())
          sys.path.insert(0, sys.path.pop(sys.path.index(local_site_packages)))
      
      set_local_bin_path()
     ```
   
7. **Craft Your Custom Conda Environment**
   - 🧪 Mix your perfect environment:
     ```bash
     conda clone pytorch-gpu <new_name>
     conda activate new_name
     conda install ipykernel
     ipykernel install <>
     conda install ...
     ```
     
8. **Vector Databases: Exploring with LanceDB**
    - 🗂️ Engage with [LanceDB VectorDB Recipes](https://github.com/lancedb/vectordb-recipes/tree/main/examples/multimodal_clip_diffusiondb)

9.**Mastery in Retrieval Augmented Generation**
   - 🎓 Learn from [LangChain](https://python.langchain.com/docs/use_cases/question_answering/) and [Llama-index](https://docs.llamaindex.ai/en/stable/getting_started/concepts.html)
 
10. **Building LLM Applications: The Ultimate Guide**
    - 📘 Deep dive into [Llama-index Docs](https://docs.llamaindex.ai/en/stable/understanding/understanding.html)

# Contributing 🤝

**Share Your Genius:**
- Fork the repository, push your changes, and open a pull request.
- Remember, every bit of contribution helps us sail further in the ocean of AI!

# Reporting Issues 🐛

**Spot Something Amiss?**
- Stumbled upon a bug or facing a challenge? Let us help! 🛠️
- Create an issue in the [GitHub repository](https://github.com/adventofmultimodal/genAI/issues) with a detailed description.
