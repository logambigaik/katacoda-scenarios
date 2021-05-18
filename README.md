# Interactive Katacoda Scenarios

[![](http://shields.katacoda.com/katacoda/klogambigai/count.svg)](https://www.katacoda.com/klogambigai "Get your profile on Katacoda.com")

Visit https://www.katacoda.com/klogambigai to view the profile and interactive scenarios

### Writing Scenarios
Visit https://www.katacoda.com/docs to learn more about creating Katacoda scenarios

For examples, visit https://github.com/katacoda/scenario-example



# Adhoc commands to practice:

# Launch the container

``  	kubectl run my-nginx --image=nginx  ```

# Expose the deployment inside of the cluster :
  
  ```` kubectl expose deployment my-nginx --port 80 ```
  
  
 ```  kubectl get all ```
 
 ![image](https://user-images.githubusercontent.com/54719289/118693829-59722e80-b803-11eb-9c63-a45f87a6fca7.png)


# How to write the right spec?
```   kubectl explain pod.spec.containers  ```


# Clean up the namespace

``` 
 kubectl get svc,pods --show-labels
 
 kubectl delete all -l run=my-nginx 
 
```
![image](https://user-images.githubusercontent.com/54719289/118694473-02208e00-b804-11eb-90d0-d5af7093f061.png)

# adhoc command to check images
```
  kubectl run web --image=loodse/demo-www
  kubectl expose deployment web --port 80 --type NodePort
```

![image](https://user-images.githubusercontent.com/54719289/118696630-66dce800-b806-11eb-834a-c134c1083f8e.png)

![image](https://user-images.githubusercontent.com/54719289/118696676-73f9d700-b806-11eb-9345-7a97e4e84dcb.png)

