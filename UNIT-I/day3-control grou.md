.control groups for resource limits

.control groups belongs to controller(giving the control) ,and it will be hlpful for sharing the resources lik network ,CPU and memory 

.namespace should be isolated in the control group 

.wihthout control group- one controller can consume all the resources(CPU RAM)

.host and other containers could crash 

.types of resources controlled by control groups:
    CPU: limit cpu usage ,assign cpu shares
    MEMORY: set max memory usage, kill container if limit exceeded
    Disk I/O: Limit read/write speed
    Network

