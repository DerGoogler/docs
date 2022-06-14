# Create Activity
How to create an Activity?

```tsx
class ChangelogActivity extends BaseActivity<Props, States> {
  public constructor(props: any) {
    super(props)
  }

  public componentDidMount = () => {
    super.componentDidMount;
    console.log(this.props.changelog.package.android);
  }

  private renderToolbar = () => {
    return (
      <Toolbar>
        <ToolbarBuilder
          title={"Changelog " + this.props.changelog.version}
          onBackButton={this.props.popPage}
          hasWindowsButtons={true}
          hasDarkMode={true}
        />
      </Toolbar>
    );
  };

  public render = () => {
    return (
      <Page modifier={native.checkPlatformForBorderStyle} renderToolbar={this.renderToolbar}>
        <ContentBody className="markdownBody">
          <div
            style={{
              padding: "16px",
            }}
          >
            <HighlightedMarkdown>{this.props.changelog.changes}</HighlightedMarkdown>
            <Button
              style={{ borderRadius: "8px" }}
              modifier="large"
              onClick={() => {
                if (native.isAndroid) {
                  native.open(this.props.changelog.package.android);
                } else if (native.isWindows) {
                  native.open(this.props.changelog.package.windows);
                } else {
                  console.log("");
                }
              }}
            >
              Download
            </Button>
          </div>
        </ContentBody>
      </Page>
    );
  };
}

export default ChangelogActivity;
```