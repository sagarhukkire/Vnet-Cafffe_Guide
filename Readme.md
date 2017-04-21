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

Thanks

