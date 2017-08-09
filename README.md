The url for the challange: http://vod.stillhackinganyway.nl/

When I checked the source code, I found the following comment:

<!-- *Knock Knock* 88 156 983 1287 8743 5622 9123 -->

After searching google for a while I understood that this probably had something to do with with "Port Knocking" and I found a write-up on another CTF challange related to "Port Knocking": https://f4l13n5n0w.github.io/blog/2015/06/21/vulnhub-knock-knock-1-dot-1/

I did some modifications to F4l13n5n0w's script:

ip = "34.249.81.124"            

def Knockports(ports):
  for port in ports:
      try:
          print "[*] Knocking on port: ", port
          s = socket(AF_INET, SOCK_STREAM)
          s.settimeout(0.5)          
          s.connect_ex((ip, port))
          print s.recv(4096)
          s.close()
      except Exception, e:
          print "[-] %s" % e

def main():
  
  r = (88,156,983,1287,8743,5622,9123)
  for comb in permutations(r):      
      print "\n[*] Trying sequence %s" % str(comb)
      Knockports(comb)
  print "[*] Done"

main()



