# Stage 1 and 2 Recycling
According to Lauren Cutlip, business development and outreach manager at the Recycling & Disposal Solutions of Virginia, there are stages to the recycling process (see https://brightly.eco/recycling-process/).  
<br/>“When the driver completes their route, they arrive at the [MRF] to be weighed in on the scale before unloading the recyclable materials onto the tip floor,” Cutlip says. “Then a loader operator will scoop the materials and fill a drum feed or hopper where the items are mixed up and brought to the presort belt where staff looks for [non-recyclable] items that could damage equipment or contaminate the end product (including wood, clothing, plastic bags, scrap metal, and food waste).”
<br/>“The materials travel through a series of mechanical sorting steps, which in the case of the RDS Roanoke single-stream facility include an OCC screen where cardboard travels up onto its own conveyor, a fine screen where glass drops out, a news screen where 2D paper is separated from 3D containers, an optical sorter that pulls out PET bottles, an overhead magnet for steel and tin cans, AMP robots that pull off HDPE containers, and—finally—an eddy current that repels aluminum cans into their designated bunker.”
<br/><br/>I break this down into Stage1 and Stage 2, respectively.  The idea is to build a computer vision model for each of the stages.  Perhaps Stage 1 model could make the staff's work safer by first having robots remove all objects about which they are reasonably certain.  
<br/></br> I've scraped about half of the data using fastai's search_images function and obtained the rest from https://github.com/garythung/trashnet
<br/>There are at least three steps that can be taken to make the model better.
<br/>As the first key step to making the model better, I would like to get more high quality images in each category, but especially more images to help differentiate plastic and glass bottles as well as paper and cardboard.  Right now a tilt in a bottle's image can 'fool' a model into thinking it's glass even if it's plastic and a 'straight' image of a plastic bottle can be mistaken for glass.  Some images of paper and cardboard can look remarkably similar, even to a person, and more images of the type that are likely to be confused by the model would help.
<br/>Secondly, I've tested the model on images it has not seen before and used those as sample images in the deployed applications.  However, a rigorous testing set for each stage is a must if it were deployed in an actual production environment.  Since this project consists of simple prototypes, I'm putting a bookmark here.  
<br/> Finally, I've trained the models locally on a 4GB GPU and settled on Resnet34.  I've tried experimenting with some of convnext or efficientnet models using the timm package (see https://www.kaggle.com/code/jhoward/which-image-models-are-best/), but I would have liked to experiment more using a better GPU in the future.  This would be less important than the previous two steps, however.   
<br/><br/> The models are deployed with Gradio on Huggingface at https://huggingface.co/spaces/dpv/Stage1Recycling and https://huggingface.co/spaces/dpv/Stage2Recycling
