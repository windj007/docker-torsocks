# docker-torsocks

Runs tor client and wraps the CMD into torsocks.
The goal is to easily get all the network connections proxied, and be able to do arbitrary number of such instances.
*Disclaimer:* spawning a net container takes quite a time due to bootstrapping, 
so it's better to wrap batch job into your program.

To get public IP of your program:

    docker run -ti --rm windj007/torsocks /test.sh


To run your program with all network connections proxied through TOR:

    docker run -ti --rm \
        -v `pwd`:/program \
        windj007/torsocks \
        /program/your_executable


To update the IP address:

    docker run -ti --rm windj007/torsocks /update_ip.sh

    
You may also want to run multiple containers simultaneously:

    for i in 1 2 3
    do
        docker run -d \
            --name crawler_$i \
            -e CRAWLER_ID=$i \
            -v `pwd`:/program \
            windj007/torsocks \
            /program/your_executable
    done


To build container:

    git clone https://github.com/windj007/docker-torsocks
    cd docker-torsocks
    docker build -t windj007/torsocks .
