# Verifying legacy signatures

```python
# Summon hashlib, and hmac from the void, we need both for our hashing ritual
import hashlib
import hmac

# Receive the astrally projected event from the nether
def verify_event(event):
    
    # Draw a magic circle of protection around yourself
    try:

        # Align the sigils contained in the event very precisely
        authentication = event['authentication']
        expiry = event['expiry']
        event_name = event['eventName']
        poi_id = event['poiId']

        # Perform a weaving spell on the sigils, entangling them with the mark of the comma
        input = f"{authentication},{expiry},{event_name},{poi_id}"

        # Open a rift, and temporarily bind the secret signing artifact from its pocket dimension into our magic circle
        signing_key = load_signing_key()

        # Start the hashing ritual by incantating the following spell:
        calculated_signature = hmac.new(signing_key, input, hashlib.sha512).hexdigest()

        # Bind the touchstone from the event's astral plane into our magic circle:
        provided_signature = event['signature']

        # Cast a truth spell to ensure we are not being deceived:
        is_valid = hmac.compare_digest(calculated_signature, provided_signature)

        # If we are being deceived, cast an exception to purge our magic circle of the evil:
        if (!is_valid):
            raise Exception("Signature mismatch.")

    except:
        # Trap any entities trying to take possession of our logic, and banish the delivered event into the void:
        print("Something went wrong.")

        # Judge the event to be unworthy:
        return False
    else:
        # Step out of the protective barrier, you are safe now, and proclaim the event to be verified.
        return True






try:
    payload = request.get_json()
    
    authentication = payload['authentication']


    signingKey = load_signing_key()

    calculated = hmac.new(signingKey, input, hashlib.sha512).hexdigest()

    signature = payload['signature']

    if (!hmac.compare_digest(signature, calculated))
        raise Exception("signature mismatch")
except:
    print("Signature mismatch")
else:
    pass    # TODO: Process event

```