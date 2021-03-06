All the images are uploaded on Docker hub in [docker-namsel-ocr](https://hub.docker.com/r/thubtenrigzin/docker-namsel-ocr/) public repository.
### Running the container
Put all the scan images in a directory in your local computer [PATH] and run the image in the background with the latest image version:
```
docker run -itd --name namsel -v [PATH]:/home/namsel-ocr/data thubtenrigzin/docker-namsel-ocr:latest bash
```
**For example** : *Path* = *~/data* and latest *tag version* = latest
```
docker run -itd --name namsel -v ~/data:/home/namsel-ocr/data thubtenrigzin/docker-namsel-ocr:latest bash
```
### Running the scripts within the container:
#### Preprocessing
Scantaillor will prepare all the images stored in your local directory *~/data*.

It is possible to add optionaly the threshold value and the double page layout by adding "l2".
```
docker exec namsel ./preprocess [threshold value] l2
```
#### Recognition
##### Pecha format
Namsel will start the recognition based on a default configuration. It uses *~/data/out* directory (the *scantaillored* images). The result file "ocr_output.txt" will be move to your working directory *~/data*
```
docker exec namsel ./pecha
```
##### Book format
Namsel will start the recognition based on a default configuration. It uses *~/data/out* directory (the *scantaillored* images). The result file "ocr_output.txt" will be move to your working directory *~/data*
```
docker exec namsel ./book
```
##### Using your own configuration with parameters
Namsel will start the recognition based on a default configuration. It uses *~/data/out* directory (the *scantaillored* images). The result file "ocr_output.txt" will be move to your working directory *~/data*
```
docker exec namsel ./namsel-ocr [parameter1 parameter2 etc...]
```

#### Automatising the recognition with the preprocess included
An all in one button for the book and pecha recognition.

The threshold preprocess value can be optionaly add as a parameter and the double page layout by adding "l2".

For the book recognition:
```
docker exec namsel ./1book [threshold value] l2
```

And for the Pecha recognition:
```
docker exec namsel ./1pecha [threshold value]
```

#### Sources of docker-namsel-ocr
Please refer to [namsel-ocr](https://github.com/thubtenrigzin/namsel-ocr) repository on Github for the source of the base built Docker image.

All the Docker source will take place on [docker-namsel-ocr](https://github.com/thubtenrigzin/docker-namsel-ocr) repository on Github.

### Realease notes:
#### v2.2.0 or latest
- add the preprocess argument "l2" for the double layout book
- check if file or directory exist before the deleting or moving actions
- stability improvements
- The script ./namsel-ocr doesn't delete the directory ./data/out after the ocr completion

#### v2.1.0
- delete the directory "out" after the recognition completion
- test if the "out" directory exists and uses the non-scantailored scan image if the preprocess has not been launched before the recognition
- use the tag "latest" for the basic image

#### v2.0.0
- add an "all in one button" for the book and pecha recognition, including the preprocessing stage
- add the threshold parameter as an option for the preprocess
- correcting an issue in book script file letting the book recognition work properly

#### v1.0.0
First release of the project