# Open a new activity

Internal activitys currently aren't shared. You should always define a activity key.

`ActivityExample` is as the main declared, for main activitys you currently don't need a toolbar

```js
import React from "react";
import { Page, Toolbar } from "@mmrl/ui";
import { Button, ListItem, ListItemIcon } from '@mui/material';
import { CloudUpload, Folder } from '@mui/icons-material';
import { useActivity } from "@mmrl/hooks";

function PickerActivity() {
  const { context, extra } = useActivity();

  const renderToolbar = () => {
    return (
      <Toolbar modifier="noshadow">
        <Toolbar.Left>
          <Toolbar.BackButton onClick={context.popPage} />
        </Toolbar.Left>
        <Toolbar.Center>{extra.title}</Toolbar.Center>
      </Toolbar>
    );
  };

  return (
    <Page renderToolbar={renderToolbar}>
      <List>
        {Array.from(Array(10).keys()).map((k) => (
          <ListItem>
            <ListItemIcon>
              <Folder />
            </ListItemIcon>
            <ListItemText primary={`File ${k}`} />
          </ListItem>
        ))}
      </List>
    </Page>
  )
}

function ActivityExample() {
  const { context } = useActivity();

  const handleOpenFilePicker = () => {
    context.pushPage({
      component: PickerActivity,
      key: "YouShouldDefineAKey",
      extra: {
        title: "Pick a file"
      }
    })
  }

  return (
    <Page>
      <Button variant="contained" startIcon={<CloudUpload />} onClick={handleOpenFilePicker}>
        Upload file
      </Button>
    </Page>
  )
}

export default ActivityExample;
```