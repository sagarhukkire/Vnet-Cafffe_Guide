Hello All !! First of all welcome to this guide. These are my experiences with 3D image segmentation ,Vnet and caffe
Hope they will be useful to you.
Let's get into topic:
1. First to use Vnet ,which kind of data you have ? medical images(volumes) in 3D, lables (that too volume in 3D, created by some tool by hand)
2. Lables must be binary as we are using dice loss in Vnet
3. Hope you have saved this images either .mha,.mhd or nrrd format, as in Vnet it is used SITK ( you can change as per your need in datamanager class)
#so we are now ready with data
4. first download 3 D caffe [https://github.com/faustomilletari/3D-Caffe]
5. Either do cmake or make to install and compile ,there is chance that after make runtest you may get error
'''
#Check failed: ExactNumBottomBlobs() == bottom.size() (3 vs. 2) SoftmaxWithLoss Layer takes 3 bottom blob(s) as input.
#ExactNumBottomBlobs is set to be 3 in the loss_layer.hpp.
'''
***change it to 2 simple isn't it?***
6. make sure you have installed 3D caffe correctly then you are ready to go
6. then download Vnet from  [https://github.com/faustomilletari/VNet]
7. go to main.py ,just create folder structure accordingly(train,test,results,snapshots) 
8. if you are using pycharm give system parameter ,-train or -test as per your need
9. if there is out of memory error coming then check 'nvidia-smi' if you are using GPU on server or reduce the data
10. Vnet converges early ,so I do not think we should train for 100000 iteration as I got nice results for 30000 then change step size
11. for more info check paper and close and open issues of Vnet .I will update this as I progress ahead with my experiments 

# Points for cmake install ,if you are stuck with make install ,try with cmake

* Go to build directory
* type ccmake ..
* there will GUI opened 
* Then press "t" to get all the possible options
* then disable CUDA_USE_STATIC_CUDA_RUNTIME (press enter to enable On or disbale OFF, on the respective flag)
* press c to configure
* press g to generate
* make all

## Hope you guys are now okay  with installation ,proper dataset and all ,let me put my experinces of my project  with Vnet,which is on way to completion
* When you are using dice loss , and your batch size is 1,2,..etc. make sure to normalize it in pylayer.py ,eitherwise caffe calculate dice loss for each volume in batch ,so instead of converging loss to 1.0 ,it goes beyond that its confusing  to understand,so please normalize (check closed issues ,there is code for it) 
* Vnet work indeed great with dice loss , but to verify your network with weighted cross entropy (U-Net has implemented it) I recommend [https://github.com/gustavla/caffe-weighted-samples] ,it has helped me to get better result too :),yes you have to add few c++ and cu files and do necessary changes, recompile again ,if you want to try weighted cross entropy
* One Note, if you see Vnet input size is 128x128x64 , and resoution too, sometimes our images does not fit to it, so your quality measures like Dice ,Jaccard result into low value, do not afraid for that. I have invested around 15 days to find out the solution, here it is. If you see your segmentation mask ,you can see there might be cuts, or full image is not available at output of network. So either pass subject of intrest  of image by cropping (taking bounding box) or add many zeros around axis and downsample (its easy one but not good quality results )

All the best
Thanks

