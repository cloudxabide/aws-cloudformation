# Tips & Tricks

## Some foo I have learned.

### Parse a "designer template" for "the goods".  
The Designer Template output contains a LOT of metadata regarding the Designer visual layout - which I don't necessarilly need.
This command will echo the lines starting with where sed finds "BEGIN" (replaced with the string you want) and complete with "END" (which.. can be anything really)
```
$ sed -n '/BEGIN/,/END/p' HexGL-designer-template.yaml
$ sed -n '/^Resources/,/EOF/p' HexGL-designer-template.yaml
```
Or better yet...
```
$ sed -n '/^Resources/,/EOF/p' HexGL-designer-template.yaml | egrep -v 'AWS::CloudFormation::Designer|id:|Metadata:'
```

### Some handy "one-liners" (they're not all one line)
Display all of the AZs in each Region
```
for REGION in $(aws ec2 describe-regions --out text --query "Regions[].RegionName"); do aws ec2 describe-availability-zones --out text --query "AvailabilityZones[].ZoneName" --region $REGION; done
```
