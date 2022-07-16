<h1 align="center">Introduction. Tunable laser.</h1>

In this project, I needed to find the optimal parameters (r, f, p) that provide the maximum intensity for different wavelengths in the single-mode regime and, finally, smooth wavelength tuning. If I can extract these parameters, I will get the tunable laser on a chip with range 30 nm.

Now, I'm going to introduce my code:

<h1 align="center"> Search of maximum λ (15k spectra).py and Map r(f, λ).py at p = 0</h1>

1) Reading each spectrum
2) Filtering (Only one peak must be in the spectrum - single-mode regime) 
  ><p>a) Deletion of spectra with weak-intensity peaks (law SNR)
  ><p>b) Deletion of parasitic signals
  ><p>c) Reading of parameters from each file
  ><p>d) Search maximum λ, intensity and full power of spectra
  ><p>e) Saving in file.txt
3) Studying the dependence between λ and parameters (r, f) according to the file.txt

<h1 align="center"><img src="https://user-images.githubusercontent.com/87599571/179037437-b62af617-8094-4c53-9e15-0406a21f5868.png" width="650" height="400" /></h1>

Actually, this map was created for the parameter **p = 0**. But, if we change this parameter, then the map will shift relative to the diagonals (Unfortunately, due to  the long experiment (about 1 month), it can be shown only for small highlighted fragment):

<h1 align="center"><img src="https://user-images.githubusercontent.com/87599571/179039394-2012c081-b859-488f-9815-7d0b494ac2e2.gif" width="350" height="300" /></h1>

To find the optimal parameters, we have to go through each diagonal of the map r(f, λ). Rather, extract the parameters in the middle of the diagonals (**See Search currents.py**). After this, we've chosen the main diagonal (**blue line**) and, furhter, only for these parameters **r** and **f**, the parameter **p** was varied.

<h1 align="center"><img src="https://user-images.githubusercontent.com/87599571/179046528-66eeeb20-70df-4080-9df1-d70525688ac1.png" width="650" height="400" /></h1>

<h1 align="center"> Variation of p for the currents of main diagonal r and f</h1>
To simplify this task, we decided to take **r** = **f** and started to change the phase (See **Map r=f (p, λ).py**). The result of this experiment can be shown on the **Map r (p,λ)**. This map contains the full data needed to change the wavelength smoothly along one diagonal. To define the parameters **p**, **r** = **f**, it was important to analyze each splice for **p** and find the middle of each shelf regarding the wavelength.

<h1 align="center">
  <img src="https://user-images.githubusercontent.com/87599571/179276650-3c0e5cea-bc09-471f-83e6-7de83e8bc9cd.gif" width="450" height="350" />
  <img src="https://user-images.githubusercontent.com/87599571/179276222-4f14d440-6e6b-4db5-9354-fe913440c7e4.png" width="500" height="350" /> 
</h1>

If we use these points from map (**r, f, p**), we will get wavelength tuning (maximum intensity of each signal):

<h1 align="center">
  <img src="https://user-images.githubusercontent.com/87599571/179351458-77f50c8b-4cf9-42e3-b7f0-f32ec3ff4bc4.gif" width="450" height="350" />
  <img src="https://user-images.githubusercontent.com/87599571/179279479-e27d985b-db2b-46fd-9f2a-05e889c6a4f0.png" width="500" height="350" /> 
</h1>

### But, there are two problems:
1) The hypothesis that the main diagonal corresponds to **r** = f wasn't correct. Actually, **r = A·func(f)**. Because of this mistake, the signals in the spectrum are worse and have wider widths (See **Adjustment of f.py**).
2) The wavelength tuning wasn't smooth. In order to have linear smooth tuning, we need to make right crosslinking.

<h1 align="center"> Adjustment of f</h1>

In the code, I decided to change **f** relative to **f = r** in the certin range. The selection criteria of f was based on the minimum spectral width and, also, the wavelength of peak in the spectrum when f is selected has to match old f = r.

<h1 align="center">
  <img src="https://user-images.githubusercontent.com/87599571/179351084-b140d653-861b-4b80-b705-7abe99095dca.png" width="450" height="300" />
  <img src="https://user-images.githubusercontent.com/87599571/179351584-4380d2be-339a-4d8d-a017-1529b1a0b511.png" width="500" height="300" /> 
</h1>

We've got the signals with smaller widths and selected appropriate parameters.

<h1 align="center"> Finish. Linear wavelength tuning. </h1>

For this task, I decided to take the old wavelength tuning with joints and remove points that deviate from the linear dependence. Then, I interpolated the resulting dependence. I've got the next parameters for the laser and this wavelength tuning:


<h1 align="center">
  <img src="https://user-images.githubusercontent.com/87599571/179353558-5e8c9c93-8c20-40c1-add6-875744e14e03.png" width="500" height="300" />
  <img src="https://user-images.githubusercontent.com/87599571/179353571-85726596-3121-4f5e-b8eb-0323bfb23671.png" width="500" height="300" /> 
</h1>
