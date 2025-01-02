# Getting started
This guide will get you started with DeviceInfo FBs. Here you will learn how to install the library into you TwinCAT environment and use the library to throughout your projects.

## Open new Project
Open TwinCAT XAE Shell and in the dialog, create a new **TwinCAT XAE Project (XML format)**, give the project a proper **Name** and **Location** and click on **Ok** to continue. The next step is to create **PLC** in your TwinCAT project by right-clicking on **PLC** in the **Solution Explorer**. In the contextmenu select **Add new item...**. In the dialog, select **Standard PLC Project**, give it a **Name** and click on **Add**.

Now lets add the library to this project. You can either install this library via Twinpack or do it manually.

## Installation via Twinpack
This library is published via Twinpack and can therefore be easily installed. If you have never used Twinpack, read through the docs at [Twinpack Repo on Github](https://github.com/Zeugwerk/Twinpack) and also on [Zeugwerk Developper Space](https://doc.zeugwerk.dev/userguide/twinpack/twinpack_quickstart.html), download the latest release and install it.

After installation right click on References and click on **Twinpack Catalog**. Click on Browse and search for DeviceInfo library. Click on it and on the right click on Add. Twinpack will now download the library and add it as reference to your project.

<div class="gallery">
  <div class="gallery-item">
    <figure>
      <img src="../images/open_twinpack.png" alt="Open Twinpack"/>
      <figcaption>TwinCAT XAE Shell</figcaption>
    </figure>
  </div>
  <div class="gallery-item">
    <figure>
      <img src="../images/login_to_twinpack_repository.png" alt="Make sure to Login to Twinpack Repository"/>
      <figcaption>Login to Twinpack Repository</figcaption>
    </figure>
  </div> 
  <div class="gallery-item">
    <figure>
      <img src="../images/add_library_to_references.png" alt="Add DeviceInfo Library to References"/>
      <figcaption>Add DeviceInfo Library to References</figcaption>
    </figure>
  </div>    
</div>

## Manual Installation
The DeviceInfo library can either be downloaded from Github as a [precompiled library](https://github.com/seehma/DeviceInfo/releases), or you can clone the [repository](https://github.com/seehma/DeviceInfo) and compile the library yourself. This guide will focus on the former usecase.

First, [get the latest release](todo) of the library, the download will give you a file called "DeviceInfo_1.0.2.1.compiled-library" on your computer. Start the TwinCAT XAE Shell or the Visual Studio Version you are usually using to develop TwinCAT PLCs. Then, in the menubar, select **PLC** and then **Library Repository...** (see figures below)

<div class="gallery">
  <div class="gallery-item">
    <figure>
      <img src="../images/open_library_manager.png" alt="Open TwinCAT Library Manager"/>
      <figcaption>TwinCAT XAE Shell</figcaption>
    </figure>
  </div>
  <div class="gallery-item">
    <figure>
      <img src="../images/select_library_and_install.png" alt="Select Library from Repository and Install it"/>
      <figcaption>Select Library from Repository and Install it</figcaption>
    </figure>
  </div>  
  <div class="gallery-item">
    <figure>
      <img src="../images/add_library_to_references_manual.png" alt="Add Library to References"/>
      <figcaption>Add Library to References</figcaption>
    </figure>
  </div>  
  <div class="gallery-item">
    <figure>
      <img src="../images/add_library_to_references_manual2.png" alt="Add Library to References"/>
      <figcaption>Add Library to References</figcaption>
    </figure>
  </div>    
</div>

In the library-repository dialog click on **Install** and navigate to the file compiled-library file and select it. Then, click on **Open** to install the DeviceInfo library into your TwinCAT environment and you are ready to use it.

## PLC
Usually you will already have a PLC, but for demonstration purposes we will start from a plain TwinCAT XAE shell. In the menubar click on **File** and then select **New > Project**.

<div class="gallery">
  <div class="gallery-item">
    <figure>
      <img src="../images/installation_twincatxae.png" alt="TwinCAT XAE Shell"/>
      <figcaption>TwinCAT XAE Shell</figcaption>
    </figure>
  </div>
  <div class="gallery-item">
    <figure>
      <img src="../images/installation_project.png" alt="Create Project"/>
      <figcaption>Create a new project</figcaption>
    </figure>
  </div>
  <div class="gallery-item">
    <figure>
      <img src="../images/installation_plc.png" alt="Add a new PLC"/>
      <figcaption>Add a new PLC</figcaption>
    </figure>
  </div>
  <div class="gallery-item">
    <figure>
      <img src="../images/installation_plc2.png" alt="Create Standard PLC project"/>
      <figcaption>Create a new Standard PLC project</figcaption>
    </figure>
  </div>  
</div>


To write your first program, which utilizes the DeviceInfo library, replace the content of the **MAIN** program by the following source code.

```st
// --- Declaration -------------------------------------
PROGRAM MAIN
VAR
  tbd
END_VAR

// --- Implementation ---------------------------------
tbd
```

> [!NOTE]
> Compiling the library yourself and as .library instead of .compiled-library will make some internal variables available to you. While this may facilates debugging 
> for tinkers , the compiled-library has purposly stripped to the variables and application engineer may find useful.
