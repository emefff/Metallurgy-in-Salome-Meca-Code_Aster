# Metallurgy-in-Salome-Meca-Code_Aster
Metallurgy-in-Salome-Meca-Code_Aster

The metallurgy of steels may also be simulated in SM/CA. Below example is a modification of test case MTLP103a. We simulate the quenching of a cylinder with D=100mm and H=100mm. Steel data is from the test case with 16MND5, a french pressure vessel steel. From the TTT-diagram data, we may expect a bainitic microstructure, just as advertised for this steel. The cylindrical specimen is left in air for 14s and subsequently  quenched in water, its initial temperature is 906°C. The tricky part in setting up such a simulation is setting up the input data from the TTT-diagram for a new steel. There is no way around properly digitzing the diagram, as they are usually not super-accurate in the first place. A second complication is the huge amount of data created, the field of CREA_META is comprised of vectors with 9 components

V1 : FERRITE
V2 : PERLITE
V3 : BAINITE
V4 : MARTENSITE
V5 : AUSTENITE
V6 : SUMCOLD
V7 : TAILLE_GRAIN
V8 : TEMP
V9 : TEMP_MARTENSITE

thus, you will need a generous amount of RAM during the simulation, even for a low number of elements (<1M elements). Let's take a look at the results of this simulation at t=240s:
![temp_240s](https://user-images.githubusercontent.com/89903493/231741288-55c82442-5c69-4693-8ef6-2bcdfe047fbb.png)

At t=240s, the center of the cylinder is still at 66°C, although we will not get any retained austenite, this gives gives you a feeling of the dimensions of the part. As we may expect from the steel datasheet, we get mostly bainite:
![bainite_240s](https://user-images.githubusercontent.com/89903493/231741649-bdf2c8b3-db8f-4622-8ea0-a41b84d56829.png)

As cooling rates are largest on the specimen surface, we can expect some martensite there:
![martensite_240s](https://user-images.githubusercontent.com/89903493/231741808-026199d6-ec4a-4149-91b6-138a4ab94ec5.png)

The hardness distribution result for this steel shows a slightly increased hardness at the surface:
![hardness_240s](https://user-images.githubusercontent.com/89903493/231742019-f0c80dc3-e767-46ef-94e1-43b8659d65ef.png)

Due to the steel's nature, do not expect any wonders there.

We noticed that accuracy of the TRC data is VERY important for the results. In an industrial setting, some calibration might be necessary.

Further refinements may be: adding the heating of the specimen to the simulation (squeeze in an additional first stage@beginning), for a case hardening steel we'd need two materials with different TTT-data (TRC1 and TRC2) and a 'layer' in the geometry for the carburized surface. 
